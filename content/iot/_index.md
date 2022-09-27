---
title: "IOT Sensors"
date: 2022-09-14T15:23:31+01:00
chapter: true
draft: false
---


## IOT Architecture ##


**Topology**

The IOT system has been designed to take sensor readings from multiple devices and link them to known cells in laboratories, this can be used to extract live experimental data or for environmental & audit purposes.

{{<mermaid align="center">}}
flowchart TD;
    A[fa:fa-satellite-dish Sensor 1] --> D(IOT Gateway)
    B[fa:fa-satellite-dish Sensor 2] --> D(IOT Gateway)
    C[fa:fa-satellite-dish Sensor 3] --> D(IOT Gateway)
    D -->  E(fa:fa-arrow-right DataFlow processing)
    E --> F[fa:fa-database BigQuery IOT Data]
    E --> G[fa:fa-bell Alerts]
{{< /mermaid >}}

 **DB Schema**

Sensors send a json packet containing the following fields.
This allows a sensor package to send readings from multiple probes at a given time.
e.g send the temperature, humidity and battery voltage.


{{<mermaid align="center">}}
classDiagram
  
    class SensorReading{
      TIMESTAMP timestamp
      STRING deviceId
      STRING sensor1Id
      NUMERIC sensor1Value
      STRING sensor2Id
      NUMERIC sensor2Value
      STRING sensor3Id
      NUMERIC sensor3Value
    }    
{{< /mermaid >}}

(timestamp and deviceId are required fields)



