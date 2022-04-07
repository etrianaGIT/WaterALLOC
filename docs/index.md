# Welcome to the WaterALLOC User Connection

## Water Resources Modeling Management System 
The original objective of this project was to develop a MODSIM-based Water Allocation Module (WaterALLOC) to be used in conjunction with the Hydro-BID modeling system, using the river basin simulation capabilities from MODSIM to enhance our river basin planning and management offerings.  The new module will allow using the hydrologic processes simulated in Hydro-BID and import them directly into MODSIM to perform simulation of water allocation and system operations, based on water use priorities, water rights, water permits, storage operation rules, and administrative and social constraints.  The new robust modeling platform will strengthen RTI’s river basin management offerings, including streamlined data management between the models, ability to simulate responses and alternatives in complex systems, evaluate water availability including priorities and operations, and evaluate impacts of climate change and benefits of adaptation measures.  

![WaterALLOC main user interface](img/GUIScreenShot_0420.png "WaterALLOC main user interface")

## Main Topics Covered

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


# Introduction

WaterALLOC is a modeling management system that provides a new geographic information system (GIS)-based interface that streamline the data processing between **HydroBID** and **MODSIM** models, offering a solution to perform water availability analysis, including river and reservoir operations with simulation of water permits and priorities, using all the river operations tools and customization provided by MODSIM. WaterALLOC was created to enhance the user experience for both, HydroBID and MODSIM users, allowing the HydroBID user to use the GIS interface to run the system and adding easy-to-use input dialogs for agricultural and municipal demands for MODSIM. Additionally, his tool creates the MODSIM simulation network automatically from the Analytical Hydrology Dataset (**AHD**) network built for HydroBID, using the catchments and streams to define the links and nodes of the MODSIM network.

<img src="img\media\image4.png" style="width:6.5in;height:3.57153in" />

WaterALLOC links the results of local runoff from HydroBID to the entry nodes of MODSIM to simulate the routing of the flows in the streams of a basin. Georeferenced demand nodes can be created within the WaterALLOC interface to simulate water intake and consumption according to water availability at different points of the basin and in accordance with the permits, priorities, and physical and hydraulic limitations of the system. Also, WaterALLOC allows the creation and simulation of operation of reservoir systems, simulating water supply and power generation operations.

The new robust modeling platform offers a streamlined solution for data management between the models, the ability to perform comprehensive water balance analysis that includes water infrastructure operation rules, water allocation priorities, and administrative and social constraints. Additionally, the platform supports scenario management allowing the simulation and analysis of dynamic changes to land cover, water demands, population, surface and groundwater interactions, and climate.

<img src="img\media\image5.png" style="width:5.94931in;height:3.67917in" />

## WaterALLOC Approach

WaterALLOC builds upon two existing modeling tools, **HydroBID** and **MODSIM** with the purpose of enhancing the ability and effectiveness in providing streamlined and comprehensive solutions for water resources management around the world. WaterALLOC brings together the hydrologic simulation capabilities from HydroBID and the river basin simulation capabilities from MODSIM to support water resources planning and management.

<table><thead><tr class="header"><th></th><th><strong>HydroBID</strong></th><th><strong>MODSIM</strong></th></tr></thead><tbody><tr class="odd"><td><strong>Function</strong></td><td>Rainfall-runoff processes modeling</td><td>River basin operation and planning modeling</td></tr><tr class="even"><td><strong>Description</strong></td><td>Highly scalable rainfall-runoff modeling system model based on the generalized Watershed Loading Factor (GWLF) formulation to estimate the availability of surface water (stream flows) at the regional, basin, and sub-basin scales.</td><td>Generic river basin management decision-support system capable of simulating complex, large-scale surface water networks; excels in the area of administering water in systems governed by water rights, administrative constraints, and agreements.</td></tr><tr class="odd"><td><strong>Features</strong></td><td><ul><li><blockquote><p>Includes the Analytical Hydrography Dataset for Latin</p></blockquote></li><li><blockquote><p>America and the Caribbean (LAC AHD), a digital representation of more than 300,000 catchments with their corresponding topography, river, and stream segments</p></blockquote></li><li><blockquote><p>Includes a GIS-based catchments and streams navigation tool</p></blockquote></li><li><blockquote><p>Provides a climate data interpolation interface to obtain rainfall and temperature inputs for the area and period of interest</p></blockquote></li><li><blockquote><p>Includes a routing scheme for quantifying time of travel and cumulative flow estimates</p></blockquote></li><li><blockquote><p>Additional modules:</p></blockquote><ul><li><blockquote><p>Simulates the effect of climate change</p></blockquote></li><li><blockquote><p>Simulate the effect of reservoirs on downstream flows</p></blockquote></li><li><blockquote><p>Link with MODFLOW groundwater models to incorporate water exchanges between groundwater and surface water</p></blockquote></li><li><blockquote><p>Model sediment loads using Modified Universal Soil Loss Equations</p></blockquote></li></ul></li></ul></td><td><ul><li><blockquote><p>Uses linear-network structure and optimization as an efficient technique to operate the system and allocate water</p></blockquote></li><li><blockquote><p>Performs water allocation based on priorities or water rights</p></blockquote></li><li><blockquote><p>Includes features for reservoirs operation</p></blockquote></li><li><blockquote><p>Allows simulation of stream-aquifer interaction and operations impacts</p></blockquote></li><li><blockquote><p>Includes customizable pre-processing, execution, and post processing</p></blockquote></li></ul></td></tr><tr class="even"><td><strong>Distribution</strong></td><td>Publicly available</td><td>Publicly available</td></tr><tr class="odd"><td><strong>Developer</strong></td><td>RTI International</td><td>Colorado State University</td></tr></tbody></table>

## WaterALLOC Key Features

-   Provides a GIS interface to visualize the catchments, streamlines, MODSIM network and results

-   Uses the AHD geo-spatial features to create the MODSIM network

-   Allows a full map of the stream network or a simplified network

-   Allows launch and run HydroBID and MODSIM from the same interface

-   Allows to perform watershed analysis (similar to the **AHD Navigation** **Tool** in QGIS)

-   Imports the output from HydroBID into the MODSIM network

-   Prepares the MODSIM network with HydroBID settings for a ready to run model

-   Allows visualizing the HydroBID output spatially in the map

-   Allows access to the MODSIM objects, functionalities, and outputs

-   Allows creating new features to complete the water allocation analysis (demands and reservoirs)

-   Provides statistical metrics and graphs to calibrate the model

-   Provides a hydro-economic module to conduct cost-benefit analysis

-   Provides a scenario management structure to address “what if” questions and develop and compare scenarios with different assumptions

<img src="img\media\image6.png" style="width:6.08333in;height:4in" />

# WaterALLOC Development

Since 2017, RTI has provided primary support for WaterALLOC development through Independent Research and Development (IR&D) Projects. Also, client-driven improvement and software customization has been conducted on project-based cases funded by the Inter-American Development Bank (IDB).

Since its initial development, WaterALLOC has been applied successfully in several countries in the Latin American and Caribbean Region (LAC) to simulate complex hydrological systems, to support long-term planning, and provide a framework for integrated water resources management.

<table><thead><tr class="header"><th><strong>Year</strong></th><th><strong>Country</strong></th><th><strong>Client</strong></th><th><strong>Status</strong></th><th><strong>Description</strong></th></tr></thead><tbody><tr class="odd"><td>2018</td><td>Peru</td><td>IDB Invest/ Danper S.A.C.</td><td>Completed</td><td>Assess water optimization activities for the Peruvian agro-industry company Danper S.A.C. located in Trujillo, Peru. Develop a water balance model to simulate the water supply and demand in the basins where Danper’s agricultural and industrial productions are located. Assess impact on the water balance considering water demand and climate variability to better understand the risk and vulnerability associated with Danper’s operations in the context of climate change. Provide a cost-benefit analysis on alternative technologies that can help mitigate water shortages and optimize the use of water. Identify green infrastructure measures focused on water collection and water storage that could be implemented in areas facing water security issues.</td></tr><tr class="even"><td>2018</td><td>Chile</td><td>IDB/Fundación Chile</td><td>Completed</td><td>Evaluate the impact of climate change on future water balance for the Maule basin.</td></tr><tr class="odd"><td>2019</td><td>Brazil</td><td>IDB/ ADASA/ANA/ CAESB/SEAGRI</td><td>Completed</td><td>Support the analysis of water supply planning for the Federal District (FD) by understanding and reducing its vulnerability to severe droughts, and by increasing the efficiency in the allocation of available water resources among different competing users, while providing a decision support tool for water resources management and water allocation. Illustrate the application of hydro-economic tools for determining efficient resource allocation and analyzing tradeoffs among competing water uses in a selected study area.</td></tr><tr class="even"><td>2020</td><td>Honduras</td><td>IDB/ UGASAM- SANAA/ENEE</td><td>Completed</td><td>Analyze the current and future conditions of water availability and scarcity for the city of Tegucigalpa in Honduras in a context of climate change, and to analyze potential water sources and different management strategies to reduce the current water deficit that faces the capital city.</td></tr><tr class="odd"><td>2020</td><td>Peru</td><td>IDB/SEDAPAL</td><td>Ongoing</td><td>Support the development of a system for the planning and integrated management of the basins that supply water to the Metropolitan Area of Lima (AML), which will seek to minimize the environmental, economic, and social impacts due to drought events.</td></tr><tr class="even"><td>2021</td><td>Colombia</td><td>IDB</td><td>Ongoing</td><td>Develop technical capacities and apply HydroBID and WaterALLOC management tools to support the formulation of Water Safety Plans for four water utilities under the IDB’s COMPASS program.</td></tr><tr class="odd"><td>2021</td><td>Chile</td><td>IDB</td><td>Ongoing</td><td>Support the development of a Drought Management Plan (DMP) for the Maipo basin that will pursue to minimize the environmental, economic, and social impacts of drought episodes.</td></tr><tr class="even"><td>2021</td><td>El Salvador</td><td>IDB</td><td>Ongoing</td><td>Provide capacity building in HydroBID and WaterALLOC modeling tools to assess the current and projected water balance in selected watersheds. Implement a water permit management module in WaterALLOC to assess water availability for existing permits in different sectors, taking into consideration the historical or projected flow regimes in a specific basin.</td></tr></tbody></table>

<img src="img\media\image7.png" style="width:5.54167in;height:5.95833in" />


