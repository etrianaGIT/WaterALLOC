# Welcome to the WaterALLOC User Connection

### Water Resources Modeling Management System 
The original objective of this project was to develop a MODSIM-based Water Allocation Module (WaterALLOC) to be used in conjunction with the Hydro-BID modeling system, using the river basin simulation capabilities from MODSIM to enhance our river basin planning and management offerings.  The new module will allow using the hydrologic processes simulated in Hydro-BID and import them directly into MODSIM to perform simulation of water allocation and system operations, based on water use priorities, water rights, water permits, storage operation rules, and administrative and social constraints.  The new robust modeling platform will strengthen RTI’s river basin management offerings, including streamlined data management between the models, ability to simulate responses and alternatives in complex systems, evaluate water availability including priorities and operations, and evaluate impacts of climate change and benefits of adaptation measures.  

![WaterALLOC main user interface](img/GUIScreenShot_0420.png "WaterALLOC main user interface")

[TOC]

## Main Sections

* Introduction 
* Getting started 
* Create a new project
* Extensions and Modules
* Working with modules 
    * General setting and options 
    * Working with [HydroBID](HydroBID_Main.md) 
    * Working with [MODSIM](Modules\MODSIM\MODSIMModule.md)
    * Hydro-Economic Module
    * GSFLow Module

## Introduction
- Description of what is WaterALLOC and motivation for its development.
    - Mutual complement of HydroBID and MODSIM
    1. WaterALLOC Approach
        - Brief explanation of HydroBID and MODSIM
        - Provide a comparison table of the features, applications (from poster)
        - Enhanced river basin management tool – make sure to have generic, accessible language and cover the big picture purpose of the tools
    2. Key Features
        - Read HydroBID input files to create the MODSIM network
        - Allows a full map of the stream network or a simplified network
        - Allows launch and run HydroBID in the WaterALLOC interface
        - Allows to perform watershed analysis (similar to the AHD navigation tool)
        - Imports the output from HydroBID into the MODSIM network
        - Prepares the MODSIM network with HydroBID settings for a ready to run model
        - Allows visualizing the HydroBID output in the map objects
        - Allows access to the MODSIM objects and outputs in the WaterALLOC interface
        - Allows creating new features to complete the water allocation analysis (Demands and Reservoirs)
        - Provides statistical metrics and graphs to calibrate the model
        - Provides a hydro-economic module to conduct cost-benefit analysis
        - Provides a scenario management structure to address “what if” questions and develop and compare scenarios with different assumptions

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        about.md  # about this documentation.
