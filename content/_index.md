---
title: "LIMS Overview"
date: 2022-09-23T14:08:21+01:00
draft: false
---

## Opencell BioHotel LIMS system


{{<mermaid align="left">}}
flowchart LR;
    A[fa:fa-user User] -->B{Client LIMS}    
    B <--> L(fa:fa-database LIMS Database)    
    B --> K(fa:fa-tasks Run manager)
    subgraph Runs      
      K --> |Inventory| C[fa:fa-shopping-cart Shopify]
      K --> E[fa:fa-calendar Equipment Booking]
      
      subgraph IOT Data
      H --> D[fa:fa-database BigQuery IOT Data]
      F(fa:fa-server IOT gateway ) --> N(fa:fa-arrow-right DataFlow processing)
      N --> D
      G(fa:fa-lightbulb Sensor Data) --> F
      end
    end
    B --> J(fa:fa-hammer Workflow Builder)
    subgraph Workflow
    J --> O(Cells)
    end
    B --> M(fa:fa-users Team Management)
    subgraph Teams
    M --> P(Subscriptions)
    M --> Q(Credits)
    M --> R(Members)
    end
    
    K --> |fa:fa-chart-line Graphs| H(fa:fa-cube Cube.js)
    N --> |fa:fa-bell Alerts| L
    
    
    
{{< /mermaid >}}
