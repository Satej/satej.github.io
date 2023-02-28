---
layout: post
title:  "Container deployment with OpenTelemetry"
date:   2023-02-28 00:00:00 +0000
categories: container deployment opentelemetry instrumentation
---

Containers help in easy localized deployment of applications but without instrumentation data it is kind of hard to understand the current state and healthiness of the container.

[OpenTelemetry](https://www.dynatrace.com/monitoring/integrations/opentelemetry/){:target="_blank"} is one such tool which helps in this area. Quoting from the [website](https://www.dynatrace.com/monitoring/integrations/opentelemetry/){:target="_blank"}:

`OpenTelemetry is an open-source CNCF (Cloud Native Computing Foundation) project formed from the merger of the OpenCensus and OpenTracing projects. It provides a collection of tools, APIs, and SDKs for capturing metrics, distributed traces and logs from applications.`

OpenTelemetry makes it easy to add instrumentation to your containers. This idea is experimented in detail explanation [here](https://www.twilio.com/blog/automatic-instrumentation-of-containerized-dotnet-applications-with-opentelemetry){:target="_blank"} gives a good reference with concepts and other details.