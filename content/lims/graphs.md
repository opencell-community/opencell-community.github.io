---
title: "Graphs"
date: 2022-09-14T16:44:34+01:00
description: "Visualise IOT data from a google cloud database"
draft: false
---


The LIMS uses [cube.js](https://cube.dev/) to visualise IOT data from the google cloud.


The cube service is connected to your cloud deployments BigQuery instance.

The cubeJS schema is as follows:


``` javascript
cube(`TemperatureData`, {
  sql: `SELECT * FROM iotsensors.temperature_data`,
  
  preAggregations: {
  },
  
  joins: {
    
  },
  
  measures: {
    count: {
      type: `count`,
      drillMembers: [deviceid, sensor1id, sensor2id, timestamp]
    },
    average1: {
      type: 'avg',
      sql: 'sensor1Value'
    },
    average2: {
      type: `avg`,
      sql: `sensor2Value`,
    }
  },
  
  dimensions: {
    deviceid: {
      sql: `${CUBE}.\`deviceId\``,
      type: `string`
    },
    
    sensor1id: {
      sql: `${CUBE}.\`sensor1Id\``,
      type: `string`
    },
    
    sensor1value: {
      sql: `sensor1value`,
      type: `number`
    },
    
    sensor2id: {
      sql: `${CUBE}.\`sensor2Id\``,
      type: `string`
    },
    
    sensor2value: {
      sql: `${CUBE}.\`sensor2Value\``,
      type: `number`
    },
    
    timestamp: {
      sql: `timestamp`,
      type: `time`
    }
  }
});

```


