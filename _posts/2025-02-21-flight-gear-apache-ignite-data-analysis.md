---
layout: post
title:  "Flight Gear Apache Ignite Data Analysis - 21.02.2025"
date:   2025-02-21 00:00:00 +0000
categories: apache ignite flight gear data analysis
---

# Connecting FlightGear with Apache Ignite for Real-Time Flight Data Monitoring

## Introduction

FlightGear is a popular open-source flight simulator, and Apache Ignite is an in-memory computing platform designed to handle large-scale, high-performance data processing. In this blog post, we will explore how to connect FlightGear to Apache Ignite and visualize real-time flight data (such as oil temperature, altitude, and engine status) using Python and Streamlit. By the end, you'll have a live dashboard that provides insights into the flight's parameters while it runs.

## Setting up FlightGear

### Downloading FlightGear

Before we dive into the code, you need to have FlightGear installed. You can download the latest version of FlightGear from [the official website](https://www.flightgear.org/download/). After downloading, extract and prepare FlightGear for use on your system.

### Running FlightGear with Telnet

Once FlightGear is set up, we need to start it with a special Telnet connection. This connection will allow us to collect real-time flight data and send it to Apache Ignite for processing. The following command will launch FlightGear with the appropriate Telnet settings:

```bash
./FlightGear-2020.3.19-x86_64.AppImage --developer=true --telnet=socket,bi,60,localhost,5500,tcp
```

Explanation of the parameters:
- `--developer=true`: Enables developer mode, which allows access to more data from FlightGear.
- `--telnet=socket,bi,60,localhost,5500,tcp`: Configures FlightGear to send data via a Telnet socket on port `5500` over TCP. The `bi` indicates bi-directional communication, meaning both reading and writing of data can happen.

### The Role of Apache Ignite

Apache Ignite is an in-memory data grid that allows us to store, query, and process data at lightning-fast speeds. By connecting FlightGear to Apache Ignite, we can store and retrieve real-time flight data efficiently.

## The Code

### Requirements

Before we begin, ensure you have the following Python libraries installed:

- `flightgear-python`: A Python interface to interact with FlightGear.
- `pyignite`: A Python client for Apache Ignite to connect and interact with the cluster.
- `streamlit`: A framework for creating interactive dashboards.

You can install the required libraries using `pip`:

```bash
pip install flightgear-python pyignite streamlit
```

### `connect_and_store.py`: Collecting Data from FlightGear and Storing in Ignite

This script connects FlightGear to Apache Ignite, collects real-time data, and stores it in the Ignite cache.

```python
import time
from flightgear_python.fg_if import TelnetConnection
from pyignite import Client
from pyignite.datatypes import CollectionObject, MapObject, ObjectArrayObject

# Initialize the Ignite client and connect to the Ignite cluster
ignite_client = Client()
ignite_client.connect('127.0.0.1', 10800)  # Replace with your Ignite server address and port

# Create or get a cache for storing the data points
cache = ignite_client.get_or_create_cache('flight_data_cache')

# Start FlightGear with the appropriate telnet configuration
telnet_conn = TelnetConnection('localhost', 5500)
telnet_conn.connect()  # Establish connection with FlightGear
type_id = MapObject.LINKED_HASH_MAP

while True:
    # Get properties for oil temperature, engine state, and altitude
    oil_temperature_str = telnet_conn.get_prop('/engines/engine/oil-temperature-degf')
    engine_running = telnet_conn.get_prop('/engines/engine/running')
    altitude_ft_str = telnet_conn.get_prop('/position/altitude-ft')

    # Convert properties to float (handle empty values)
    oil_temperature = float(oil_temperature_str) if oil_temperature_str else 0.0
    altitude_ft = float(altitude_ft_str) if altitude_ft_str else 0.0
    timestamp = time.time()

    # Prepare the data to store in Ignite
    data_point = {
        'timestamp': timestamp,
        'oil_temperature': oil_temperature,
        'altitude_ft': altitude_ft,
        'engine_running': engine_running
    }
    
    cache.put(int(timestamp), (type_id, data_point))

    # Print the data for monitoring
    print(f"Oil Temperature: {oil_temperature:.1f} °F")
    print(f"Altitude: {altitude_ft:.1f} ft")
    print(f"Engine Running: {engine_running}")

    # Sleep before the next data collection
    time.sleep(1)

# Close Ignite client connection when done
ignite_client.close()
```

### `app.py`: Visualizing Flight Data in Real Time

The `app.py` script fetches data from the Apache Ignite cache and uses Streamlit to display it in a live dashboard.

```python
import streamlit as st
import time
import pandas as pd
from pyignite import Client
from pyignite.datatypes import MapObject
import matplotlib.pyplot as plt

# Initialize the Ignite client and connect to the Ignite cluster
ignite_client = Client()
ignite_client.connect('127.0.0.1', 10800)  # Replace with your Ignite server address and port

# Get the cache where data is being stored
cache = ignite_client.get_cache('flight_data_cache')

# Streamlit setup
st.title("Flight Data - Real-time View")
st.write("Displaying real-time flight data (oil temperature, altitude, and engine status)")

# Create a placeholder for the plot
placeholder = st.empty()

# Real-time data collection
while True:
    df = pd.DataFrame(columns=['timestamp', 'oil_temperature', 'altitude_ft', 'engine_running'])
    
    # Fetch the last 100 keys from the cache
    data_points = []
    current_time = int(time.time())
    
    for offset in range(100):
        key = current_time - offset
        if cache.contains_key(key):
            data_point = cache.get(key)[1]  # The data point is the second item in the tuple
            data_points.append(data_point)
    
    # If there are data points, convert them into a DataFrame
    if data_points:
        new_data = pd.DataFrame(data_points)
        new_data = new_data.sort_values(by='timestamp', ascending=True)
        
        # Keep only the latest 100 entries
        df = pd.concat([df, new_data], ignore_index=True).tail(100)

    # Plot the data
    fig, ax = plt.subplots()

    ax.plot(df['timestamp'], df['oil_temperature'], label='Oil Temperature (°F)', color='tab:red')
    ax.plot(df['timestamp'], df['altitude_ft'], label='Altitude (ft)', color='tab:blue')

    ax.set_xlabel('Timestamp')
    ax.set_ylabel('Values')
    ax.set_title('Flight Data (Oil Temperature & Altitude)')
    ax.legend(loc='upper right')

    # Update the Streamlit plot
    placeholder.pyplot(fig)

    # Sleep before the next update
    time.sleep(1)

# Close Ignite client connection when done
ignite_client.close()
```

### How It Works

1. **Collecting Data from FlightGear**: The `connect_and_store.py` script uses the FlightGear Python interface (`flightgear-python`) to collect oil temperature, altitude, and engine status. These parameters are sent over Telnet to the Apache Ignite cluster.
2. **Storing Data in Ignite**: The data is stored in an Apache Ignite cache, with the timestamp as the key and the flight data as the value.
3. **Visualizing Data**: The `app.py` script fetches the latest data points from the Ignite cache and displays them on a real-time dashboard using Streamlit. The dashboard continuously updates with the most recent data.

## Running the System

### Step 1: Start FlightGear
Run FlightGear with the Telnet configuration specified above.

```bash
./FlightGear-2020.3.19-x86_64.AppImage --developer=true --telnet=socket,bi,60,localhost,5500,tcp
```

### Step 2: Run the Data Collection Script
Execute `connect_and_store.py` to start collecting data from FlightGear and sending it to Apache Ignite:

```bash
python connect_and_store.py
```

### Step 3: Launch the Streamlit Dashboard
To visualize the flight data, run the following command:

```bash
streamlit run app.py
```

The dashboard will now display real-time data for oil temperature, altitude, and engine status as FlightGear continues running.

## Conclusion

In this blog post, we’ve learned how to connect FlightGear to Apache Ignite, collect real-time flight data, and visualize it using Streamlit. This system provides an interactive and powerful way to monitor flight parameters in real-time and make data-driven decisions. You can further extend this setup by adding more data points, optimizing performance, or deploying it for more complex simulations.
