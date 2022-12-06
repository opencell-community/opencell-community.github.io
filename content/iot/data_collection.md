---
title: "Data Collection"
date: 2022-09-16T12:31:26+01:00
draft: true
---

# Sensor Data


The sensors are configured to use the DHT11, DHT22 and Onewire sensor protocols.

These readings are taken at fixed intervals transmitted to the google cloud IOT gateway.

The sensor wakes once a minute to take a reading and send via an HTTP request.


Each data packet is of the form 

``` json
{
    "timestamp" : "2022-02-02T12:43:22",
    "deviceID": "abc",
    "sensor1Id": "mysensor1",
    "sensor1Value": 12.44,
    "sensor2Id": "def",
    "sensor2Value": 31.44
}
```