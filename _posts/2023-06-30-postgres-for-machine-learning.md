---
layout: post
title:  "Postgres for Machine Learning"
date:   2023-06-30 00:00:00 +0000
categories: database postgres LLM machine learning
---
Machine learning is definitely picking up with the advent of LLMs. There are different ways to access LLMs to power your applications:
1. Using an API as a service similar to ChatGPT
2. Hosting your own LLMs and passing your inputs through them

One other way LLMs are being used is close to where data resides which is in the databases. Many data vendors like Google Bigquery, Databricks, Snowflake have found a way to run user inputs/requests by executing them in a SQL query where they are calling a particular function which accesses a LLM to process the input. While this is a nice feat, they are more proprietary in nature.

[PostgresML](https://github.com/postgresml/postgresml){:target="_blank"} is a machine learning extension to PostgreSQL that enables to perform training and inference on text and tabular data using SQL queries.

As per extract from the github site:
```
PostgresML is a machine learning extension to PostgreSQL that enables you to perform training and inference on text and tabular data using SQL queries. With PostgresML, you can seamlessly integrate machine learning models into your PostgreSQL database and harness the power of cutting-edge algorithms to process data efficiently.
```

I tried running it on my personal laptop and it was a very smooth experience in installing and trying the sample notebooks which come in handy with the UI page along with the installation. Defintely recommend everyone to give it a try. The github page is very self-explanatory to install and try it out using docker-compose.