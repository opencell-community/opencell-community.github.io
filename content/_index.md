---
title: "LIMS Overview"
date: 2022-09-23T14:08:21+01:00
draft: false
---

## Opencell BioHotel LIMS system

Welcome to the docs site for the opencell-community [GitHub](https://opencell-community.github.com).

Here we document the software architecture and hardware state of the management system for the [BioHotel](https://www.opencell.bio/labs/start) concept.

On the left are sections which go into further detail regarding the various subsystems.


### Overview

The BioHotel LIMS system is a 1-stop shop for building and managing life science research and production workflows. It allows users to design experiments with regards to equipment and consumables, execute parts of the experiments remotely, collect data from a range of sensors and use the cost effective shared infrastructure to more effectively grow and scale biotech startups.

This system lives as a digital twin to the physical BioHotels and is designed to allows teams to collaborate on experiments and more quickly get to the point that research can be commercialised.



### Key Concepts

 **Cell**

 A Cell is a contained discrete process which may require certain inputs and may produce outputs.
 Cells are the building blocks of the BioHotel concept, a cell can be chained to other cells to produce a workflow.
 Cells are used as the basis of the scheduling system and the inventory management system.

 Cells can represent the execution of a particular assay, a preparation of a sample, an analysis of a sample or many other use cases.

 Examples of cells include:

  - DNA extraction
  - DNA sequencing
  - PCR testing
  - Liquid handling 
  - Cell culture
  - Autoclave
  - Centrifuging
  - Gel electrophoresis

Cells are the representations of services provided by a BioHotel. Initially cells are from services provided locally.

Cells have a cost of use which can be set in a number of different ways, initially the cost of the consumables plus a fixed price.

 
 **Workflow**

 A workflow is a collection of cells chained together to take an input and produce an output.
 The workflow is linked to a user who is in a team.
 Workflows cost of execution is a function of the total cost of running the necessary cells.
 Workflows create a directed graph of cells and their execution order.

 **Run**


### Architectural overview



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
