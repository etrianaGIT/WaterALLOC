<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

# WaterALLOC User Manual

Version 2.4


# WaterALLOC Software Installation

WaterALLOC is distributed at no cost to our clients. To install WaterALLOC, copy the installation files into a folder and run the installer by double clicking the **setup.exe** file and then click on Install in the prompt window.

<img src="img\media\image8.png" style="width:6.5in;height:2.35in" />

When installation has completed successfully, you can open the program by searching for WaterALLOC in the Start menu of Windows and then clicking on the program icon <img src="img\media\image9.png" style="width:0.55974in;height:0.4375in" />.

RTI provides a free license to use the software for non-commercial purposes. The license is granted for 30 days and it is automatically renewed with an Internet connection every 30 days.

WaterALLOC runs in Microsoft Windows computers with a minimum of XX RAM capacity and an Internet connection is not required.

<img src="img\media\image10.png" style="width:0.44792in;height:0.44792in" /> **Note**: Although it is not required to install MODSIM in your computer, several versions of MODSIM are also distributed within the program installation files. Having MODSIM installed can be useful for editing complex networks.

# WaterALLOC Workspace

The workspace refers to the location where all inputs files, model executables, databases, and supplemental information related to a WaterALLOC project are saved. In other words, it is the location of the **Project Folder**. When a new project is created in WaterALLOC, users need to specify the directory of the Project Folder or can make a new folder in a specified location, and the WaterALLOC project file (.waprj) and two subfolders named “HydroBID” and “MODSIM” will be automatically created and saved in the Project Folder. In the HydroBID folder there will be all executable and settings files needed to run the model and a subfolder named “WALLOCFiles” where all HydroBID output files in .csv format will be stored. The HydroBID folder can also be set through the HydroBID main menu in WaterALLOC (see [Section](#set-up-hydrobid-folder) 6.2.1). All the MODSIM .xy files used in the WaterALLOC project and the output files (in a sqlite database) will be stored in the MODSIM folder. It is suggested that all the shapefiles that are used in the project are stored in a subfolder within the Project Folder, such as “GIS” to avoid problems with the visibility of the layers uploaded in the map when opening the WaterALLOC project from a different directory or a different computer.

<img src="img\media\image12.png" style="width:5.42708in;height:2.375in" />

# HydroBID and MODSIM Modeling Tools

To get started, we suggest getting familiarized with the following key concepts about HydroBID and MODSIM.

## HydroBID Overview

The HydroBID modeling system for quantitative simulation of hydrology and climate change has three primary components: the **Analytical Hydrography Dataset (AHD)**, the **database**, and the **hydrologic model**.

### AHD

The **AHD** is a digital representation of catchment boundaries and stream segments for the entire LAC region, containing over 300,000 catchments with an average size of 83 km<sup>2</sup> for South America and 23 km<sup>2</sup> for Central America and the Caribbean. The AHD is a regional platform of spatial data used to integrate the disparate data needed to support hydrologic modeling. It provides a framework for consistently parameterizing models, provides the necessary river network connectivity, and stores the data necessary for displaying results in a GIS format (Rineer and Bruhn, 2013).

### COMID

Each of the catchments and stream segments delineated in the AHD has a unique identifier number known as **COMID**, which allows to quickly identify the basins and rivers that drain at a certain point within the extension of the AHD.

> <img src="img\media\image13.png" style="width:6.5in;height:4.02222in" />

### AHD Flow Table

HydroBID includes a table containing the upstream/downstream relationship between each stream or each catchment. The table with this information is the **AHD flow table (AHDFlow.dbf**). This table allows the navigation of the AHD using GIS tools and in the WaterALLOC interface.

### Database

The **database** contains information associated with each catchment, including drainage area, stream length, slope, land uses, soil types, and climate. Additionally, each catchment in the AHD is parametrized with land use and soil type data from global datasets. The land cover data is based on the U.S. Geological Survey (USGS) Global Land Characterization and the soil type data is based on the Harmonized World Soil Database (HWSD) supported by the International Institute for Applied Systems Analysis (IIASA) and the Food and Agriculture Organization (FAO). The catchment’s soil and land cover conditions determine the Curve Number (CN) and the hydrologic soil group that the model uses to calculate runoff. All the input data for HydroBID, including climate tables, is stored in a single SQLite database.

> <img src="img\media\image14.png" style="width:6.5in;height:2.84861in" />

### Hydrologic Model

The **hydrologic model** is an enhanced version of the rainfall-runoff Generalized Watershed Loading Function (GWLF) model (Haith and Shoemaker, 1987), coupled with a novel lag-routing methodology developed by RTI (Moreda et al., 2014). The model computes runoff and baseflow by catchment. The GWLF estimates runoff using the U.S. Soil Conservation Service’s curve number (CN) method. Catchment CNs are stored in the database and are determined by the watershed’s combination of soil and land cover conditions, which are represented as hydrologic soil groups, cover type, treatment, and hydrologic condition. After runoff estimates, excess precipitation infiltrates to the unsaturated layer where it is subject to evaporation. Over time, the infiltrated water percolates from the unsaturated layer downward to replenish the saturated storage. Water within the saturated layer enters the stream channel as baseflow where it combines with runoff from the catchment and any inflows from the upstream catchments to provide the stream flow volume, which is then routed through the stream network defined by the AHD (Add Reference to Technical Note 2).

> <img src="img\media\image15.png" style="width:5.09375in;height:3.45833in" />

### Climate Data Interpolation Tool 

A preprocessor referred to as the Climate Data Interpolation Tool (**CDIT**), built into the HydroBID modeling system, automates spatial interpolation of daily temperature and precipitation time series between stations. The tool uses the Inverse Distance Weighting (IDW) method to interpolate climate data at the centroid of each catchment.

### Outputs

HydroBID can simulate stream flows in unimpaired watersheds for historic, current, and future conditions based on land use, precipitation, and temperature inputs. **Model outputs** of predicted streamflow are saved in readily usable, comma separated value (.csv) format, at either a daily or monthly time step. The system has a graphical user interface (GUI) to facilitate loading and processing of model input, as well as to display both graphical and tabulated model output.

> <img src="img\media\image16.png" style="width:6.5in;height:4.02917in" />

The hydrologic model utilizes the data structure and the catchment and stream network topologies of the AHD to generate flow estimates at the outlet of any catchment or basin selected by the user. In addition to flow generation, HydroBID includes other modules for 1) reservoir simulation, 2) sediment transport, and 3) surface and groundwater interactions using MODFLOW.

### Calibration Parameters

HydroBID contains several calibration parameters that are used to adapt the model and optimize its performance simulating observed streamflows. HydroBID provides default values for some of the hydrologic parameters in the database. For instance, the database contains values for the CN and for AWC in the vadose zone. However, these parameters need to be calibrated to historical streamflow measurements by modifying a factor that multiplies the values already contained in the database. For other parameters, such as the recession (r) and seepage (s) coefficients, the user needs to enter the initial values that will be applied uniformly to all catchments within the simulated area.

<img src="img\media\image17.png" style="width:6.5in;height:5.97778in" />

The table below provides a list of the calibration parameters and the suggested value range.

<table><thead><tr class="header"><th><strong>Parameter</strong></th><th><strong>Description</strong></th><th><strong>Suggested Value Range</strong></th></tr></thead><tbody><tr class="odd"><td>Curve Number (CN)</td><td>Controls the initial amount of abstraction used to calculate runoff. Default values are available in the database.</td><td>0.8–1.2 (multiplier)</td></tr><tr class="even"><td>Available Water Capacity (AWC)</td><td>Enables the start of percolation from the unsaturated layer to the saturated layer. Default values are available in the database.</td><td>0.2–1.2 (multiplier)</td></tr><tr class="odd"><td>Recession Coefficient (r)</td><td>Control base flow rate.</td><td>0.001–0.75<br />
(day<sup>-1</sup>)</td></tr><tr class="even"><td>Seepage Coefficient (s)</td><td>Controls the rate of percolation to the deep saturated zone.</td><td>0.005–0.1<br />
(day<sup>-1</sup>)</td></tr><tr class="odd"><td>Evapotranspiration Factor (ET) in the Growing Season</td><td>Evapotranspiration factor during the growing season.</td><td>0.5–1.5</td></tr><tr class="even"><td>Evapotranspiration Factor (ET) in the Latent Season</td><td>Evapotranspiration factor during the dormant season.</td><td>0.5–1.5</td></tr><tr class="odd"><td>Temperature Threshold</td><td>Temperature below which precipitation is assumed to be snow and above which accumulated snow will melt.</td><td><p>-1–4</p><p>(°C)</p></td></tr><tr class="even"><td>Melting Factor</td><td>Factor controlling the rate at which snow melts.</td><td><p>0.3–0.6</p><p>(mm day<sup>-1</sup> °C<sup>-1</sup>)</p></td></tr></tbody></table>

### Settings File

HydroBID saves all the setting parameters provided in the GUI into a text file (.txt). This **setting file** allows an identical re-run of the model at any time in the future. When open HydroBID, the GUI will be automatically populated with the values in the setting file, and all required data for a model run will be obtained from the current folder.

## MODSIM Overview

MODSIM, developed by the Colorado State University, is a decision-making support system that uses optimization in a stream network to help watershed managers with the analysis of water supply in the face of hydrological uncertainty and demand growth (<http://modsim.engr.colostate.edu/>). As a decision support system, MODSIM is designed for developing improved strategies for short-term water management, long-term operational planning, drought contingency planning, water rights analysis and water allocation between urban, agricultural, and environmental sectors (Labadie, 2012). The model uses the concept of flow networks to efficiently simulate complex water systems at river basin scale.

One of the advantages of MODSIM is that it can be customized for any unique basin management conditions, specialized operating rules, input data, output reports, and access to external models running concurrently with MODSIM, all without having to modify the original MODSIM source code. In addition, RTI holds a collaboration agreement to support the maintenance and development of MODSIM and provide our clients with enhanced and long-term support.

> <img src="img\media\image18.png" style="width:4.56965in;height:3.24758in" />

Below are some of the key MODSIM capabilities. Labadie, 2012 has a complete list of the software capabilities.

### Network Flow Optimization

The basic solver in MODSIM is a state-of-the-art network flow optimization algorithm that is more than an order of magnitude faster than solvers currently in use in other river basin modeling packages and capable of modeling extremely large-scale networks. The optimization of stream network provides an efficient way assuring allocation of flow in accordance with specified rights and priorities.

### Data-driven Model

MODSIM maintains complete reliance on user input data and specifications for describing system features, operational requirements, and priorities, which are separated from the network modeling algorithmic structure. No a priori defined operating policies or priorities hardwired into MODSIM.

### Long-term Planning to Real-time Operations

MODSIM is applicable to long term planning (monthly), medium term management (weekly), and short-term operations (daily) in river systems.

### Complex River Basin Configurations

Complex network topologies can be constructed, including looped and bifurcating flow paths. Network topology is graphically created by simple point and click actions on the GUI palette. In addition, georeferenced network topologies can be loaded into MODSIM from a geographic information system (GIS).

### Reservoir Operations and Hydropower Generation

Reservoir balancing routines are included, allowing division of reservoir storage into several operational zones for controlling the spatial distribution of available storage in a river basin. Hydropower generation capacity and energy production is based on power plant efficiencies varying with discharge and head. Energy production calculations are performed, with consideration of tailwater effects and head-dependent hydraulic capacity restrictions on reservoir discharge.

### Conjunctive Use

MODSIM includes modeling capabilities for conjunctive use of surface water and groundwater and simulation of stream-aquifer interactions. A stream aquifer model based on the USGS sdf approach is included, as well possible linkage with external groundwater models.

### Water Rights and Storage Contracts

MODSIM is capable of directly incorporating institutional structures governing water allocation under direct flow or natural streamflow rights and seasonal storage rights and contracts, including provisions for allocating water according to specified priorities based on current river basin conditions.

### Customized MODSIM 

Users are provided access to all key variables and object classes in MODSIM, thereby allowing customization for any complex river basin operational and modeling constructs without the need for reprogramming and recompiling the MODSIM source code. Custom code can be developed for defining complex operating rules and policies, executing external modules such as water quality models, input of specialized data sets for particular applications, preparing customized model output and reports, and linking MODSIM with database management systems to provide access to timely data and forecast information for real-time river basin management.

The physical water resource systems are represented as a network of nodes, both storage (i.e., reservoirs) and non-storage (i.e., stream confluences, diversion points, and demand locations), and links (i.e., canals, natural river reaches).

<img src="img\media\image19.png" style="width:5.83333in;height:2.68109in" />

> Some of the key characteristics and example applications of MODSIM are:

<table><thead><tr class="header"><th><strong>Features</strong></th><th><strong>Selected Application Examples</strong></th></tr></thead><tbody><tr class="odd"><td><ul><li><blockquote><p>Uses linear-network structure and optimization as an efficient technique to operate the system and allocate water</p></blockquote></li><li><blockquote><p>Performs water allocation based on priorities or water rights</p></blockquote></li><li><blockquote><p>Includes features for reservoirs operation</p></blockquote></li><li><blockquote><p>Allows simulation of stream-aquifer interaction and operations impacts</p></blockquote></li><li><blockquote><p>Includes customizable pre-processing, execution, and post processing</p></blockquote></li></ul></td><td><ul><li><blockquote><p>Long-term water supply planning: “Planning under deep uncertainty”</p></blockquote></li><li><blockquote><p>Evaluation of salinity recovery strategies</p></blockquote></li><li><blockquote><p>Analysis of alternative infrastructure option for water supply</p></blockquote></li><li><blockquote><p>Water rights yield and third-party effects</p></blockquote></li><li><blockquote><p>Investigation of impacts of ecological flows enforcement</p></blockquote></li><li><blockquote><p>Optimization of reservoir operations, including hydropower</p></blockquote></li><li><blockquote><p>Water availability studies for operation expansion or sustainability</p></blockquote></li></ul></td></tr></tbody></table>

# WaterALLOC Features and Functionalities

## WaterALLOC GUI

The WaterALLOC interface consist of a **map window** to visualize the physical features of the study area and the MODSIM network elements; a **main menu** at the top, providing access to HydroBID and MODSIM functionalities; a **toolbar menu** that provides one-click access to various GIS and other program functions; a **log messages window** that records all the actions performed by the user and also shows error messages; a **project** **settings window** that is used to set the configurations of a WaterALLOC project and allows access to scenario management and view; and a **layer explorer panel** shown in the left side of the interface that allows to hide/show all layers available and to customize their properties.

<img src="img\media\image20.png" style="width:6.5in;height:3.71042in" />

### Main Menu

The main menu provides access to the most important functions of WaterALLOC.

<img src="img\media\image21.png" style="width:4.32292in;height:0.25in" />

-   **File:** Allows to create a new WaterALLOC project, open an existing project, and save changes made to a project.

-   **Options**: Allows to switch between English and Spanish languages and to activate WaterALLOC modules, such as the [hydro-economic module](#hydro-economics-tools).

-   **View**: Allows to activate the different windows of the WaterALLOC interface.

-   **HydroBID**: Allows access to the [AHD Navigation](#hydrobid-tools) tool, which allows to navigate downstream/upstream the catchments and river segments and perform a watershed analysis, to the [HydroBID simulation](#_HydroBID_simulation) to set the configurations of the model run (i.e., sqlite, climate data, observed streamflow files, calibration parameters, etc.) and view the results. Also, allows access to the [create MODSIM network](#_HydroBID_simulation) and [import HydroBID output](#import-hydrobid-output) windows.

-   **MODSIM**: Allows access to MODSIM network settings and to run the model.

-   **MMS**: Allows access to the optimization module.

-   **Tools**: Allows to import a layer from a comma separated value (.csv) file.

-   **Help**: Includes the license agreement and the WaterALLOC version, and allows access to the user manual.

### Toolbar Menu

The toolbar menu provides access to some GIS functions and MODSIM available elements.

> <img src="img\media\image22.png" style="width:6.5in;height:1.06736in" />

<table><thead><tr class="header"><th><strong>This Icon</strong></th><th><strong>Is Used to:</strong></th></tr></thead><tbody><tr class="odd"><td><img src="img\media\image23.png" style="width:0.27083in;height:0.22917in" /></td><td>Add layers to the map</td></tr><tr class="even"><td><img src="img\media\image24.png" style="width:0.26042in;height:0.22917in" /></td><td>Move the map to progressively display adjacent areas</td></tr><tr class="odd"><td><img src="img\media\image25.png" style="width:0.27083in;height:0.25in" /></td><td>Select objects displayed in the map window. To select an object, make sure to select the layer in the Layer Explorer Panel on the left.</td></tr><tr class="even"><td><img src="img\media\image26.png" style="width:0.27083in;height:0.23958in" /></td><td>Zoom in the map</td></tr><tr class="odd"><td><img src="img\media\image27.png" style="width:0.25in;height:0.26042in" /></td><td>Zoom out the map</td></tr><tr class="even"><td><img src="img\media\image28.png" style="width:0.26042in;height:0.22917in" /></td><td>Zoom to the previous extent</td></tr><tr class="odd"><td><img src="img\media\image29.png" style="width:0.26042in;height:0.21875in" /></td><td>Zoom to the next extent</td></tr><tr class="even"><td><img src="img\media\image30.png" style="width:0.26042in;height:0.21875in" /></td><td>Zoom to maximum extent</td></tr><tr class="odd"><td><img src="img\media\image31.png" style="width:0.27083in;height:0.23958in" /></td><td>Zoom to coordinates</td></tr><tr class="even"><td><img src="img\media\image32.png" style="width:0.23958in;height:0.22917in" /></td><td>Identifies features of the selected object in the map</td></tr><tr class="odd"><td><img src="img\media\image33.png" style="width:0.25in;height:0.23958in" /></td><td>Show the attribute table of selected layer. Also allows to query the selection of features</td></tr><tr class="even"><td><img src="img\media\image34.png" style="width:0.21875in;height:0.1875in" /></td><td>Select label</td></tr><tr class="odd"><td><img src="img\media\image35.png" style="width:0.28125in;height:0.25in" /></td><td>Enable/disable basemap</td></tr><tr class="even"><td><img src="img\media\image36.png" style="width:0.25in;height:0.26042in" /></td><td>Select local inflows</td></tr><tr class="odd"><td><img src="img\media\image37.png" style="width:0.25in;height:0.21875in" /></td><td>Enable/disable MODSIM layers</td></tr><tr class="even"><td><img src="img\media\image38.png" style="width:0.23958in;height:0.21875in" /></td><td>Demand Node. Add consumptive demands (i.e., agricultural, domestic, groundwater pumping). Demand nodes can also be added by importing a shapefile or a .csv file</td></tr><tr class="odd"><td><img src="img\media\image39.png" style="width:0.19792in;height:0.22917in" /></td><td>Reservoir Node. Add reservoirs for modeling reservoir storage operations and hydropower generation</td></tr><tr class="even"><td><img src="img\media\image40.png" style="width:0.25in;height:0.21875in" /></td><td>Nonstorage Node. Simulate catchment runoff, which are imported from the outputs of HydroBID. Add tributary inflows, water transfers, groundwater return flows</td></tr><tr class="odd"><td><img src="img\media\image41.png" style="width:0.25in;height:0.22917in" /></td><td>Sink Node. Basin outlet</td></tr><tr class="even"><td><img src="img\media\image42.png" style="width:0.20833in;height:0.21875in" /></td><td>Link. Add maximum and minimum flow, stream channel losses</td></tr><tr class="odd"><td><img src="img\media\image43.png" style="width:0.29167in;height:0.25in" /></td><td>Remove MODSIM nodes and links</td></tr><tr class="even"><td><img src="img\media\image44.png" style="width:0.23958in;height:0.20833in" /></td><td>Stop editing mode</td></tr></tbody></table>

### Project Settings Window

The settings or project preference window shows the active scenario in the WaterALLOC interface and provides the absolute or relative paths to the configuration files of a WaterALLOC project and scenarios. It is divided in three main tabs:

-   *General* tab shows the absolute path to the workspace and allows to select the flowline layer.

-   *Hydro-BID* tab shows the relative paths to the HydroBID .jar (executable) file, the [AHD Flow table](#ahd-flow-table), and to the HydroBID [settings file](#settings-file).

> <img src="img\media\image10.png" style="width:0.44792in;height:0.44792in" />**Note**: When creating a WaterALLOC project (.waprj), a HydroBID folder is automatically created in the same workspace, which includes HydroBID executables and a **WALLOCFiles** subfolder that organizes outputs files of HydroBID runs for different scenarios. Also, a folder for the Default scenario and its respective **settings file** is automatically created.
>
> <img src="img\media\image45.png" style="width:5.47974in;height:2.18194in" />

-   *MODSIM* tab allows access to an existing MODSIM network file or allows to create a new .xy file. It also allows to modify the coordinate scaling factors, which are used to convert the GIS coordinates to the MODSIM interface canvas.  Depending on the GIS projection used, the user might have to experiment with the convenient set of values to comfortably display the network in MODSIM.

<img src="img\media\image46.png" style="width:6.5in;height:2.96736in" />

The project settings window also allows to hide/show the scenarios management panel. See [Section 6](#scenarios-management) for more information about the scenario management.

<img src="img\media\image47.png" style="width:6.5in;height:1.4875in" />

### Layer Explorer Panel

All layers added to a WaterALLOC project will be displayed in the layer panel on the left. The panel helps manage the display order of map layers and their symbology and set other properties of each map layer. Layers listed at the top are displayed first, followed by the layers below them. A layer’s attribute information can be accessed by clicking the attribute table icon (<img src="img\media\image48.png" style="width:0.28125in;height:0.23958in" /> ) or the Identifier icon (<img src="img\media\image49.png" style="width:0.25in;height:0.22917in" />) in the toolbar menu. When creating a WaterALLOc project, the MODSIM Network layers and the Online Basemap are automatically loaded to the panel. These layers should not be removed. Use the check box to the left of each layer to turn it on or off. Right-click on the layer to zoom to layer, export all or selected features, set labels, and access the Properties dialog window to change the symbology.

<img src="img\media\image50.png" style="width:2.88542in;height:3.44792in" />

## HydroBID Tools

WaterALLOC offers different HydroBID tools that can be accessed through the [**HydroBID** main menu](#main-menu). Below, there is a description of the functionalities of each of the HydroBID tools.

### Set up HydroBID Folder

This option will prompt a window where the user can navigate to the [workspace](#wateralloc-workspace) or project directory and set a HydroBID folder. A folder named “HydroBID” will be created, and the model executables files together with a WALLOCFiles subfolder will be automatically saved within this folder.

<img src="img\media\image51.png" style="width:6.5in;height:4.06875in" />

### Set Inflow Points

The **Set Inflow Points** tool allows flagging inflow points in the flowline layer. It creates a field named ***IsFlowPnt*** in the attribute table of the flowline layer shapefile.  The tool needs a field COMID to identify the objects to flag. The field **IsFLowPnt** is created the first time that the tool is used, if it does not exist. The tool stacks the map selected features in the "Selected COMIDs" list and provides the buttons <img src="img\media\image52.png" style="width:0.56528in;height:0.2176in" /> to add and remove the listed features from the list of inflow points. The “Label” is automatically filled in, adding the sufix “\_Inf” to the COMID. The label can be edited by the user. The Label is used to name the MODSIM non-storage node representing the inflow point.

<img src="img\media\image53.png" style="width:6.5in;height:2.68403in" />

Once inflow points are set, the properties of the streamline shapefile can be changed to display Inflow Points in different color and width using the Highlight Inflow Points icon (<img src="img\media\image54.png" style="width:0.29167in;height:0.22917in" />).

<img src="img\media\image55.png" style="width:6.5in;height:2.93611in" />The flow simulated at the Inflow Points is the aggregate flow of all upstream catchments (COMIDs) plus the flow of the catchment where the inflow point is selected. For instance, from the figure below the flow at each of the three Inflow Points (INP) is mathematically represented as follows. Note that the colors of the catchments represent the area that contributes to a specific INP.

*F**l**o**w* *a**t* *I**N**P* 1 = Flow<sub>307676500</sub> + Flow<sub>307668700</sub> + Flow<sub>307668800</sub>

*F**l**o**w* *a**t* *I**N**P* 2 = Flow<sub>307578700</sub> + Flow<sub>307562200</sub> + Flow<sub>307586600</sub>

*F**l**o**w* *a**t* *I**N**P* 3 = Flow<sub>307635600</sub> + Flow<sub>307621100</sub> + Flow<sub>307601400</sub> + Flow<sub>307586700</sub> + Flow<sub>307668800</sub>

<img src="img\media\image56.png" style="width:6.5in;height:3.98889in" />

### Precipitation and Temperature Processing

These set of tools allow processing and visualizing the HydroBID meteorology data in the HydroBID database. The spatial processing tools allows calculating mean aerial estimates of precipitation and temperature for each catchment in the study area and summarize the results into the HydroBID database. The spatial data processing tool includes a historical data processing mode and a forecast data processing mode. The visualization tool displays the available datasets in the database and allows generating plots and tables of the precipitation and temperature time series for each of the catchments, identified by the COMID. User interface uses the current scenario HydroBID settings file to load the data available in the referenced database.

#### Spatial Processing of Historical Data

The spatial processing is performed using an ***R*** script that performs the areal operation. ***R*** needs to be installed and operational in the computer to perform these tasks in WaterALLOC. The path of the ***R*** executable is preset in WaterALLOC to the default location, however, if R is installed in a different location, it can be selected using the browse <img src="img\media\image57.png" style="width:0.20899in;height:0.18939in" alt="Graphical user interface, text, application, email Description automatically generated" /> button. The spatial data processing is performed for the selected *Catchments Layer* domain. The data in the NetCDF rasters should cover the *Catchments Layer* extends.

<img src="img\media\image58.png" style="width:6.48815in;height:5.01447in" alt="Graphical user interface, text, application, email Description automatically generated" />

#### Spatial Processing of Forecast Data

#### Data Visualization

\[Work in progress - ET\]

### AHD Navigation

WaterALLOC includes a tool that allows to browse AHD catchments and streams with the capability of navigating upstream and downstream and selects a set of catchments that belong to a given watershed. This **AHD Navigation Tool** is useful to identify the drainage area of a basin for simulation, for which the tool requires the identification of the most downstream AHD catchment. Once the downstream catchment is provided, the system navigates the database ([AHDFlow.dbf](\l)) and collects all the catchments within the basin. The tool is run through the “Watershed Analysis” button and yields information about the count of catchments navigated, total area in square kilometers, the length of all flowlines in kilometers, and provides a list of the COMIDs of all catchments selected.

<img src="img\media\image59.png" style="width:6.5in;height:3.675in" />

### HydroBID Simulation

HydroBID is a standalone program written in Java but can be launched and run through the WaterALLOC GUI using the **HydroBID Simulation** tool. The user needs to identify the most downstream catchment (COMID) of the basin that will be simulated in HydroBID. Additionally, observed flow time series can be imported to an existing link in the MODSIM network to facilitate comparison with the simulated flows. The inflow point files can also be search for or generated.

Once the COMID has been selected or loaded, the HydroBID Simulation window shows general preferences, such as the location of the AHD flow database and the workspace, and preferences for the selected scenario, including the settings file, flow file, and output folder. Users have two options to run HydroBID. The first option is by launching the HydroBID GUI using the button “*Launch Hydro-BID GUI*” and the second option is by executing the model in a batch mode with the “*Execute Hydro-BID*” button. The first option enables to make changes to the configurations (e.g., changing calibration parameter values) before running the model, whereas the second option runs the model with the configurations in the settings file. The option “*Set all- catchments output*” might be selected to obtain outputs for each of the catchments within the simulated basin.

<img src="img\media\image60.png" style="width:6.5in;height:3.44583in" /><span id="_HydroBID_simulation" class="anchor"></span>

Once HydroBID is run successfully, the output files are stored in the **WALLOCFiles** folder and in the folder for the active scenario. WaterALLOC populates the output file names for the HydroBID runs using the scenario name and the COMID.

<img src="img\media\image61.png" style="width:6.5in;height:3.05833in" />

### Create MODSIM Network

The **Create MODSIM Network** tool offers two options to automatically create a MODSIM network that represents the simulated basin. The *“All catchments”* option creates a network with inflow points (Nonstorage MODSIM nodes) for <u>all</u> the catchments within the study area. This option allows to create a network that matches the AHD stream network. On the other side, the *“Only inflow points”* option allows creating a simplified MODSIM network with only the local inflow locations (previously identified with the [Set Inflow Points](#set-inflow-points) option) representing the hydrologic inflows (NonStorage nodes). The latter option is useful when simulating big watersheds where there is no need to have a detailed network and inflows can be aggregated at key locations.

<img src="img\media\image62.png" style="width:4.84375in;height:5.62154in" />

To create a MODSIM network, the most downstream catchment needs to be selected. In the dialog window, the COMID of the catchment is visible, and general and MODSIM network preferences are shown, such as the active scenario, path of the workspace, name of the MODSIM file, and the streamline layer. Additionally, the window includes the option to append a network to an existing MDSIM network. If the “*Append to existing network*” is uncheck, WaterALLOC will replace any current network with the newly created.

<img src="img\media\image63.png" style="width:4.13542in;height:4.2969in" />

### Import HydroBID Output

One of the main functionalities of WaterALLOC is streamline the connection between HydroBID outputs and MODSIM inputs to provide efficiency in the use of the combined features of both models. Through the **Import HydroBID Output** tool, users can import outputs from HydroBID into the MODSIM network. The available output to be imported will be shown in the window, which is tied to the active scenario in the WaterALLOC GUI. Available outputs appear in different rows and can be identified by the RunName.

There are several output variables than can be imported. In the **To MODSIM** tab, the tool will import the “Generated Flow m3/day”, which refers to the simulated flow generated at each catchment, to the MODSIM network. When MODSIM is executed, flows will be then routed through the hydrologic network until reaching the Sink node. When importing outputs for “*All catchments*”, HydroBID had to be run for all catchments, so each of the catchments has its respective output file. If the “*Overwrite MODSIM Settings*” option is selected, the MODSIM Network Settings (e.g., time step and simulation period) are replaced with the configuration in the [HydroBID setting file](#settings-file). Note that once simulated flows are imported, units are adjusted to the MODSIM default units (1000 m<sup>3</sup>/day).

<img src="img\media\image64.png" style="width:5.38542in;height:5.61458in" alt="Graphical user interface, text, application, email Description automatically generated" />

In addition to importing the Generated Flow simulated in each catchment, this tool allows to import groundwater seepage simulated also with HydroBID, which can be used to approximate the underneath aquifer recharge. When the option “*Import groundwater seepage*” is selected, WaterALLOC processes the HydroBID seepage into the MODSIM network. The first time this option is used in the network, it creates a MODSIM reservoir at upstream end of the most downstream catchment to simulate the aquifer water balance and connects each catchment with the reservoir to simulate the groundwater seepage as a daily volume of water, multiplying the seepage depth by the area of the catchment, which is taken from the *Catchment Shapefile* and the *Area Column* field specified by the user. The processing of seepage increases the inflows to the non-storage nodes to simulate inflows including the seepage and the surface runoff. The groundwater seepage links are set up between the inflow nodes and the reservoir representing the aquifer with a -300,000 cost to guarantee that seepage is simulated from the non-storage inflow, leaving only the surface runoff in the surface network.

Once the network includes the seepage network construct nodes and links, the HydroBID import tool can import the surface water runoff only or both the surface runoff and the seepage to the MODSIM inflow nodes. In the case the seepage links exist and the use elects to not include the seepage, these links will be closed during the import operation and only surface water runoff will be processed to the non-storage inflow nodes.

***Overwrite MODSIM Settings***: When activated will use the simulation preferences defined in HydroBID to set the MODSIM simulation period and daily time step. It will also assign an accuracy of two decimal digits by default.

***Import Monthly Time Series***: When activated it will process the daily HydroBID results into a monthly time series with average flows (m3/day) for the entire month. This option should only be used if the MODSIM simulation is intended to be in a monthly time step.

***Clear all MODSIM inflows***: This option will clear all the non-storage nodes inflow time series in the entire network (not only the basin to be proceeded) before processing and importing the HydroBID time series. Caution should be used in multi-basin MODSIM networks to avoid losing other flows imported into the network.

<img src="img\media\image65.png" style="width:6.5in;height:4.25208in" />

Results simulate natural recharge to the aquifer (represented with the reservoir node) from natural processes. The Upstream Inflows to the reservoir sum the total aquifer recharge.

> <img src="img\media\image66.png" style="width:4.80903in;height:3.26111in" />

In addition to import outputs to MODSIM, the **Weather to DB** tab allows to import weather data from the [HydroBID database](#database) to the WaterALLOC database for all catchments (all COMIDs) or for a selected COMID. This is useful when estimating net water demand for irrigation, so agricultural demand considers the precipitation data used in HydroBID to estimate the irrigation requirements. The precipitation imported will be provided as options in the agricultural demand nodes regardless of the spatial location.

Furthermore, the **Spatial Import** tab allows to import any HydroBID output variable to be visualized in the map window of the WaterALLOC GUI. This feature enables to visualize the spatial distribution of modeled flows and other output variables within the basin.

<img src="img\media\image67.png" style="width:6.5in;height:3.53542in" />

## MODSIM Tools

### Creating MODSIM Networks

There are different ways to create MODSIM networks to work with WaterALLOC: 1) using the HydroBID AHD, 2) using a shapefile with unique identifiers, and 3) loading a previously created MODSIM network. The first option is described in [Section](#create-modsim-network) 6.2.6. The second option can be accessed through the MODSIM main menu and then selecting **Network Utilities**. This option needs a shapefile with a unique field (e.g., COMID) and a filed with the drainage area. These two fields need to be selected in the **Create Network** tab. The drainage area information is stored in the project database (.waprj) in a table called “wateralloc\_runoffSupp”. This table is associated with each scenario and contains the MODSIM GUID associated with the element originally created and the associated drainage area. When user click on the “Create Network” button, the tools will create a non-storage node for each unique feature in the shapefile.

<img src="img\media\image68.png" style="width:6.5in;height:3.41597in" />

<img src="img\media\image69.png" style="width:2.62826in;height:2.37391in" />A simplified network can also be created in the **Topology Tools** tab, using inflow points previously set with the [Set Inflow Points](#set-inflow-points) tool.

*Explain about Network Adjustments tab….*

The third option to create a MODSIM network in waterALLOC is loading a previously created network. In the tab **MODSIM** in the **Project Preference** window, users can navigate to a specific MODSIM file (.xy) by clicking in the yellow folder icon.

<img src="img\media\image70.png" style="width:6.5in;height:1.13958in" />

### Setting MODSIM Elements

Once a MODSIM network is created in WaterALLOC representing the natural hydrologic dynamic of the basin, the network can be complemented with other MODSIM elements, such as demands and reservoirs, to characterize different interventions, developments, and operations occurring within the basin.

The WaterALLOC GUI provides spatially referenced capabilities that allow to add and link basin network elements on the display, and then populate data for that element by right-clicking to open the dialog window form associated with that element. The [Toolbar Menu](#toolbar-menu) at the top of the GUI contains several MODSIM elements icons, such as demands, reservoirs, non-storage, and sink nodes for adding them in the network by clicking on the icon and then clicking on the desired location in the Map Window.

<img src="img\media\image71.png" style="width:6.5in;height:0.47083in" />

#### Demands

There are three options to parametrize water demands ( ) in WaterALLOC:

-   **Option 1: Manually through the demand node properties dialog**

<img src="img\media\image72.png" style="width:1.9375in;height:1.625in" />Right clicking on a demand node and selecting “*MODSIM*” opens a dialog window of the node properties. In the "*Time Series*" tab, the volume of water used can be added, which can be defined as historical diversions, water concessions, agricultural, municipal and industrial demands based on consumptive use calculations carried out outside of MODSIM.

The demanded water volume can be entered manually or by copying and pasting the time series. Selecting “*Varies By Year*” allows to enter time series for different years; not selecting it allows demand patterns to repeat annually. There are other complex operations, such as groundwater pumping, infiltration, and return locations that can be set through the node properties window as well.

<img src="img\media\image73.png" style="width:2.98958in;height:4.3008in" />

-   **Option 2: Manually through the WaterALLOC data entry dialogs**

    -   *Add mathematical equations to calculate demands using data input through WaterALLOC dialogs*

<img src="img\media\image74.png" style="width:1.92708in;height:1.54167in" />WaterALLOC displays data entry dialogs that allow to parametrize agricultural and municipal water demands by clicking in the “*Agriculture*” or “*Domestic*” options at the node. Data entered in the dialog windows is used to calculate the volume of water demanded for MODSIM runs.

-   **Agriculture Demands** can be defined by “*User Defined*” crop parameters or by “*Crop-based*” default parameters stored in the WaterALLOC database (.waprj).

> The “*User Define*” option allows to estimate agriculture demand using the following parameters, per crop (one node can be composed by a single or multiple crops).

-   Total Irrigated area (ha)

-   Crop label

-   Percent of crop irrigated area (%)

-   Total annual demand (in thousand cubic meters per hectare - 1000 m<sup>3</sup>/ha)

-   Monthly distribution of annual demand (%/month). There are two default monthly patterns for corn and wheat crops, which can be edited or used to create new ones.

> <img src="img\media\image75.png" style="width:4.33654in;height:5.125in" />
>
> The “*Crop-based*” option allows to estimate agriculture demand based on preset crop water requirements for different growth stages, which are stored in the WaterALLOC database (.waprj). Users can select a crop from the dropdown menu list and the crop coefficient (Kc) values and planting month will be automatically loaded in the dialog window. The list of crops, their respective Kc values, and development stages were obtained from Allen et al. (1998) and are stored in the WaterALLOC database in the “wateralloc\_croptype”, “wateralloc\_cropcoeffic”, “wateralloc\_cropdevelopmentstage” tables, respectively.
>
> The user-input required data are:

-   <img src="img\media\image76.png" style="width:3.45208in;height:4.63542in" />Total irrigated area (ha)

-   Crop label

-   Percent of crop irrigated area (%)

This option also allows to input parameters used in the [**Hydro-economics Tools**](#hydro-economics-tools), such as crop price, yield response factor, maximum yield, and annual production costs.

<img src="img\media\image77.png" style="width:6.5in;height:4.15347in" />

The net irrigation water requirement (NIWR) for the node is computed using the input parameters, and is shown in table and graphical formats, under the “*Timeseries*” and “*Plot*” tabs, respectively. When the *“User Defined”* option is selected, precipitation data from HydroBID are made available to compute the portion of the water requirement supplied by rain; the remaining water required is the NIWR for the node. Precipitation time series are imported when HydroBID is executed and stored in the WaterALLOC database to be available to the demand nodes. The combined NIWR for all the crops in a demand node becomes the MODSIM demand, that is, water that is requested from the stream network and allocated by MODSIM based on priorities and simulation of operations.

<img src="img\media\image78.png" style="width:6.5in;height:3.53819in" />

-   **Municipal Demands** can be defined by four user-input parameters. Each raw in the dialog window can represent a municipality, city, town, district, or zone (i.e., urban, suburban, rural).

    -   Total population

    -   Area label

    -   Percent of population area (%)

    -   <img src="img\media\image79.png" style="width:3.73958in;height:4.41951in" />Total annual demand (gallon per capita per day - gpcd)

    -   Monthly distribution of annual demand (%/month). There is a default monthly pattern for household, which can be edited or used to create new ones.

The WaterALLOC Agriculture and Municipal dialog windows also show the total water demand for the node calculated using the input parameters, in table and graphical formats, under the “*Timeseries*” and “*Plot*” tabs, respectively.

For Agricultural demands, WaterALLOC offers the option to

Weather variables from Hydro-BID are made available to compute the net irrigation water requirement (NIWR).  These variables are imported when Hydro-BID is executed and stored in the WaterALLOC database to be available to the demand nodes.  The weather is selected in the demand nodes in the 'Time Series' tab, along with the option to enable NIWR calculations

-   **Option 3: Automatically through the WaterALLOC Demands Import tool**

<img src="img\media\image80.png" style="width:2.09184in;height:0.70408in" />This option is useful for large networks with numerous demands (e.g., water permits). Instead of adding and parametrizing each demand node individually, clicking on the black arrow next to the demand icon in the Toolbar Menu and then on Import with WaterALLOC Demands Data… displays the **Demands Import Tool** dialog window that automatically creates and imports demand data into a MODSIM network to be visualized in the Map Window of WaterALLOC. The tool preserves existing elements of the network and creates demand nodes by three type of uses (agricultural, municipal, or others) and by COMID. The preferences of the active scenario are shown in the tool, including the MODSIM .xy file.

<img src="img\media\image81.png" style="width:6.5in;height:4.09722in" />

Demand data needs to be prepared and organized in a comma separated value (.csv) file, which requires the following parameters.

<img src="img\media\image10.png" style="width:0.44792in;height:0.44792in" /> **Note**: Column labels in the file need to be exactly as appears in the table. The file may contain additional information, but it requires data for the 10 required input parameters.

<table><thead><tr class="header"><th><strong>Parameter</strong></th><th><strong>Column Label in the .csv File</strong></th></tr></thead><tbody><tr class="odd"><td>Unique identification number for each water permit</td><td>OBJECTID</td></tr><tr class="even"><td>COMID where the water permit is located (can be obtained with GIS spatial analysis tools)</td><td>COMID</td></tr><tr class="odd"><td>Type of use (Agricultural “Agrario”, municipal “Poblacional”, and others “Otros”)</td><td>Uso</td></tr><tr class="even"><td>Annual demand (m<sup>3</sup>)</td><td>Demanda Anual (m3)</td></tr><tr class="odd"><td>Type of crop</td><td>Crop</td></tr><tr class="even"><td>Irrigated area (ha)</td><td>Area irrigada (ha)</td></tr><tr class="odd"><td>Population</td><td>pop_sum</td></tr><tr class="even"><td>Agricultural demand per hectare (1000 m<sup>3</sup>/ha)</td><td>Annual Demand Ag (1000 m3/ha)</td></tr><tr class="odd"><td>Percent of water use per month (%)</td><td>%Volume_1, %Volume_2, %Volume_3, …Volume_12</td></tr><tr class="even"><td>Volume of water used per month (m<sup>3</sup>/month)</td><td>Volumen_1, Volumen_2, Volumen_3, …Volumen_12</td></tr></tbody></table>

Below is an example of a water permits data organized with the required headings.

<img src="img\media\image82.png" style="width:6.5in;height:1.93958in" />

The **Demands Import Tool** dialog window also allows to set the priorities for the type of nodes. A value of one (1) means the highest allocation priority and a value of three (3) the lowest. *Explain how the code used this info to calculate the cost….*

<img src="img\media\image83.png" style="width:3.16667in;height:1.13816in" />Furthermore, the tool provides options to configure return flows, which is useful for modeling efficiency in irrigation and municipal water distribution systems. For instance, a 60% consumption with a lag time of seven (7) days for agricultural demands, means that 40% of the allocated water is returned to the network within the next following seven days.

*Explain all the features included in “Set Demands” option under the MODSIM main menu.*

<img src="img\media\image84.png" style="width:4.875in;height:2.74635in" alt="A screenshot of a computer Description automatically generated with medium confidence" />

#### Reservoirs

The red triangle node ( ) is used to represent reservoirs in a MODSIM network. The reservoirs can be parametrized with the following key characteristics.

<table><thead><tr class="header"><th><strong>Required</strong></th><th><strong>Optional</strong></th></tr></thead><tbody><tr class="odd"><td><ul><li><blockquote><p>Maximum and minimum volume</p></blockquote></li><li><blockquote><p>Initial volume</p></blockquote></li><li><blockquote><p>Reservoir target storage</p></blockquote></li></ul></td><td><ul><li><blockquote><p>Evaporation rate</p></blockquote></li><li><blockquote><p>Groundwater seepage rate</p></blockquote></li><li><blockquote><p>Area/Capacity-Elevation curve</p></blockquote></li><li><blockquote><p>Hydropower characteristics</p></blockquote></li></ul></td></tr></tbody></table>

The of Reservoir Target Storage represent the top of the active or conservation storage pool of the reservoir. MODSIM allows the conservation pool to be divided into several operational zones which serve to improve regulation of storage levels in multi-reservoir systems. In addition, the Reservoir Target Storage is used for calibrating MODSIM by specifying target storge levels as measured historical data and then adjusting different model parameters to match observed streamflow records. To achieve relatively balanced storage among several reservoirs in a basin, each reservoir should have the same priority (set in the General tab) and similar incremental costs (se in the Targets tab under Reservoir Layer Priorities).

Users have the option to enter net evaporation rates in the Reservoir Node Properties window, which are defined as evaporation rates minus rainfall rates. Negative entries signify that rainfall rates exceed evaporation rates for that time period. MODSIM accepts a variable number of elevation-area-storage-hydraulic outlet capacity data points for any reservoir, which are interpolated to calculate reservoir surface area corresponding to any current volume in the reservoir. Evaporation loss is calculated in MODSIM as a function of average surface area in a reservoir over the current period (refer to MODSIM user manual for more details).

Seepage is assumed to be a function of average volume in the reservoir over the current period and the seepage loss rate is assumed to be constant. In contrast with evaporation losses, a portion of reservoir seepage may be contributed to downstream return flows. The seepage loss fraction is entered in the Groundwater Seepage tab. Entry of aquifer parameters or return flow lag coefficients allows calculation of downstream return flows from reservoir seepage.

<img src="img\media\image85.png" style="width:6.5in;height:5.46458in" alt="Graphical user interface Description automatically generated" />

#### Delete MODSIM Elements

Any MODSIM element can be deleted with the (<img src="img\media\image43.png" style="width:0.21875in;height:0.1875in" />) button. To delete an element, make sure to select the layer of the element that needs to be deleted in the Layer Explorer Panel in WaterALLOC to avoid simultaneously deleting multiple elements. When unwanted elements have been removed, make sure to click the (<img src="img\media\image44.png" style="width:0.23958in;height:0.20833in" />) button to stop the editing mode on WaterALLOC.

### MODSIM Network Settings

<img src="img\media\image86.png" style="width:1.83333in;height:1.80208in" />MODSIM network settings can be accessed through the *MODSIM* Main Menu. In the General tab, users can specify a number of options. For instance, they can select the desired accuracy for data input and flow results can be either integer accuracy or 2-place decimal accuracy. Users can select either English or metric units, with the default units used for storage, flow, head, net evaporation rates and hydropower specified. However, users may input data in any desired units in the node and link properties windows, and MODSIM will automatically convert the data to the default units.

The Time Step tab allows to specify either monthly, weekly, or daily simulation

time steps. Start Date and End Date for time series data entered into MODSIM must

be the same for all data including inflows, demands, reservoir storage targets, etc.

However, a MODSIM simulation run can start and end at any intermediate dates, as

specified in the Simulation Start Date and Simulation End Date. This is useful, for example, when calibrating the model using a subset of the historical data set.

<img src="img\media\image87.png" style="width:6.5in;height:4.48333in" alt="Graphical user interface Description automatically generated" />

### Cost Analysis

<img src="img\media\image88.png" style="width:2.03061in;height:2.82398in" />The Cost Analysis option under the *MODSIM* Main Menu displays the Network Overview form providing a tabular listing of all nodes and links in the network. Clicking the radio button next to Links lists all links and gives information on the link Type and Cost and clicking the radio button next to Nodes lists all demand and reservoir nodes and gives information on the node Type and Priority. The form provides a convenient way, particularly for large networks with numerous demand and reservoir nodes, to edit Node Priorities or Link Costs without having to select the node object in the WaterALLOC Map Window and display its properties form. In addition, a number of Table Queries are available for displaying only those nodes that satisfy particular criteria for evaluation.

<img src="img\media\image89.png" style="width:6.5in;height:5.37847in" alt="Graphical user interface, application Description automatically generated" />

### Run MODSIM

Once the system network has been created and the database populated, MODSIM can be executed from the WaterALLOC interface under MODSIM &gt; Run MODSIM. The “**standard MODSIM Run**” is the default MODSIM run and should be used when there are not extensions selected. The “**Hydroeconomic Analysis**” run is only displayed when selecting the “Hydro-Economics” extension under the Main Menu *Option &gt; Extensions*. The later option should be used only when applying the [Hydro-economic Tools](#hydro-economics-tools).

<img src="img\media\image90.png" style="width:3.6344in;height:2.63542in" alt="Graphical user interface, application Description automatically generated" />

### MODSIM Priorities to Allocate Water

In MODSIM, optimization is primarily conducted as a means of accurately simulating the allocation of water resources in accordance with operational priorities based on system objectives, operational experience, water rights, and other ranking mechanisms, including economic factors. The objective function in MODSIM is set to minimize the product between the flow rate (q) and cost (c) (weighting factors, or water right priorities per unit flow rate) in all links. The **Cost** defines the preference or priorities for moving water. Rather than their absolute values, it is the relative order or ranking of the negative costs that determines how MODSIM allocates network flows. It is important to note that the solution accumulates costs in the network for flow paths. For example, in the two networks below, the amount of water (q=50) available at the non-storage node A will primary flow the path towards node D because the cumulative cost of the links between nodes A and D is higher than the cumulative cost of the links between A and F.

<img src="img\media\image91.png" style="width:6.5in;height:2.1375in" alt="Chart, line chart Description automatically generated" />

## Hydro-economics Tools

To support hydro-economic analysis, RTI developed a module that leverages the WaterALLOC user environment and database to organize and store the economic data. It uses the MODSIM customization features to perform economic benefit calculations based on the MODSIM water allocation simulation, and it leverages the MODSIM output system to store the results of the economic analysis for each time step. The result is a module that integrates inputs, output, and scenario management through the WaterALLOC interface.

The hydro-economic methods implemented in WaterALLOC considers three main water use sectors: agriculture, municipal supply, and hydropower. For each type of water use, the model estimates, in monetary terms, the benefits of water use. More precisely, it estimates the net benefits associated with the amount of water supplied to each water user to fulfill the sector’s purpose, because it also allows the user to account for and deduct the costs associated with each water use activity.

<table><thead><tr class="header"><th><strong>Sector</strong></th><th><strong>Net Benefit</strong></th></tr></thead><tbody><tr class="odd"><td>Agriculture</td><td>Revenue from crops produced with irrigation, net of production costs</td></tr><tr class="even"><td>Municipal Supply</td><td>Value of water supply to domestic users, net of delivery costs</td></tr><tr class="odd"><td>Hydropower</td><td>Revenue from electricity generation, net of operation costs</td></tr></tbody></table>

Given these sector-specific benefits, the model then estimates the aggregate (i.e., combined) benefits of any user-specified water allocation scenario, by summing net benefits across the different water uses and nodes within the system. These aggregate benefits can be estimated for each period specified in the model and can be further aggregated across periods and expressed as a present value.

Therefore, the model provides results that allow the user to directly compare the aggregate benefits of different water allocation scenarios. In other words, the user can see how aggregate benefits increase or decrease from one allocation scenario to another.

In addition, this module allows users to assess the cost–benefit implications of specific projects that permit different water allocations within the system. For example, it can be used to assess infrastructure projects that expand irrigated area or improve irrigation efficiency. For these types of applications, the user specifies the main cost components for the project (e.g., capital, operation and maintenance \[O&M\]) and the corresponding water allocation, and the model generates results comparing the present value of project costs with the present value of changes in aggregate water use benefits.

### Agricultural Sector

For the agricultural sector, WaterALLOC allows defining the water needs as a function of one or multiple crops in a water demand node, using two options: 1) the user can specify the annual crop water requirement and a monthly pattern for each crop, or 2) specify the crops with their associated irrigated area to estimate the crop water requirement based on the crop growth stages and characteristics.

#### Crop Water Requirement

WaterALLOC assumes that the crop water requirement (***ETc***) can be supplied by rainfall, irrigation, or a combination of the two. The calculation uses daily rainfall from a user-specified precipitation time series to estimate the portion of the water requirement supplied by rain, while the remaining water required is the net irrigation water requirement (NIWR) for each crop. The combined NIWR for all the crops in a demand node becomes the MODSIM demand, that is, water that is requested from the stream network and allocated by MODSIM based on priorities and simulation of operations.

While in option 2, ***ET<sub>c</sub>*** is provided by the user, under option 1, ***ET<sub>c</sub>*** can be calculated using the following equation:

<table><tbody><tr class="odd"><td><span class="math display"><em>E</em><em>T</em><sub><em>c</em></sub> = <em>K</em><sub><em>c</em></sub> E<em>T</em><sub>0</sub></span></td><td>Eq. 1</td></tr></tbody></table>

Where:

> ***K<sub>c</sub>*** is the crop coefficient (unitless), which varies by crop type, climate, soil evaporation, and crop growth stages. Use and typical values of this coefficient can be found in Allen et al. (1998).
>
> ***ET<sub>o</sub>*** is estimated crop reference evapotranspiration and is estimated using the Blaney–Criddle equation, which is a function of the temperature and daytime hours (Allen and Pruitt, 1986):

<table><tbody><tr class="odd"><td><span class="math display">ETo = <em>p</em> (0.457<em>T</em><sub>mean</sub> + 8.128)</span></td><td>Eq. 2</td></tr></tbody></table>

> ***T<sub>mean,\ </sub>***is the mean daily temperature (°C) as the average of the maximum and minimum temperatures.
>
> ***p*** is the mean daily percentage of annual daytime hours.

#### Crop Annual Yield Function

***Y<sub>x\ </sub>***is the (maximum) annual crop yield (in ton/ha/year), when the crop water requirement is fully met over the growing season. This maximum yield is considered a local factor because it depends of multiple factors, including soils, practices, climate, and others, and it is usually obtained from historical production records. ***Y<sub>a</sub>*** is the actual annual crop yield (in ton/ha/year), depending on the actual water applied and effective rainfall. Vaux and Pruitt (1983) define the relationship between the maximum yield and the actual yield as:

$\\left( 1 - \\frac{Y\_{a}}{\\text{Yx}} \\right) = K\_{y}\\left( 1 - \\frac{\\text{ET}\_{a}}{\\text{ETx}} \\right)$ Eq. 3

Where:

> ***K<sub>y</sub>*** is the crop yield response factor (unitless), representing the effect of a reduction in evapotranspiration on yield losses. The *K<sub>y</sub>* concept and application guide can be found in Steduto et al. (2012)
>
> ***ET<sub>a</sub>*** is the actual annual evapotranspiration (in meters) and is represented by the water received by the crop from both rainfall and irrigation.
>
> ***ET<sub>x</sub>*** is the annual crop water requirement that yields ***Y<sub>x</sub>*** (in meters). This value is assumed to be equal to ***ET<sub>c</sub>*** when no water constraints exist.

For each crop, for the irrigated area in the demand node, the yield function as a function of the volume of water required and supplied in a year can be written as:

<table><tbody><tr class="odd"><td><span class="math display">$$\left( 1 - \frac{Y_{a}}{\text{Yx}} \right) = K_{y}\left( 1 - \frac{\sum_{i = 1}^{\text{\ D}}\left( \left( \text{Pp}_{i}*A \right) + S_{i} \right)}{\sum_{i = 1}^{D}{{\text{ET}_{x}}_{i}*A}} \right)$$</span></td><td>Eq. 4</td></tr></tbody></table>

Where:

> ***A*** is the irrigated area for this crop (in hectares).
>
> ***S<sub>i</sub>*** is the supply from surface irrigation simulated in MODSIM for this crop for day ***i*** in .cubic meters Note there could be multiple crops in the same demand node, so the total supply to the demand node is distributed proportional to the irrigated land included in the node.
>
> ***Pp<sub>i</sub>*** is the precipitation for day ***i*** (in cubic meters per hectare).
>
> ***D*** is the number of days in the year.

#### Economic Benefit

With the annual production ***Y<sub>a</sub>*** (tons/ha/year) for each crop, the economic benefit (net benefit in monetary units) is calculated using the market crop price, the production costs, and the area irrigated for each crop.

*N**e**t* *B**e**n**e**f**i**t* = (*Y*<sub>*a*</sub>(*P*) − (*C*<sub>*p*</sub>))*A* Eq. 5

Where:

> ***P*** is the crop market price (in monetary units per ton).

***C<sub>P</sub>*** is the cost per hectare per year to produce the crop, including O&M and irrigation costs.

#### User Inputs in WaterALLOC

The user input to evaluate net benefits include, for each crop:

-   Crop price ($/ton)

-   Yield response factor (***Ky***)

-   Maximum yield (tons/ha/year)

-   Annual crop production cost ($/ha/year)

These inputs are provided by demand nodes that represent a single or a collection of agricultural water demands.

<img src="img\media\image92.png" style="width:6.26042in;height:4.07997in" />

In addition, for each node, the user can include cost components for water projects that will affect the supply or demand for water in the agricultural sector. In particular, the user can specify: 1) the “capital cost,” representing the one-time costs incurred in the initial stage of a project and 2) O&M costs representing the ongoing costs incurred annually for the life of the project. O&M costs can be defined either as fixed annual monetary value or as a percentage of the capital costs.

<img src="img\media\image93.png" style="width:2.95311in;height:3.44792in" />

### Municipal Sector

For public water supplies, the benefit from providing potable water to residences is represented using estimated economic demand curves for water, combined with cost estimates for alternative sources of water.

Unlike the water “demand” terms previously used in this report to describe a fixed amount of water required by a user group, the *economic demand curve* for water is a functional relationship (***D***) representing the amount of water that a household ***k*** would be willing and able to purchase during a time period *t* (***w<sub>kt</sub>***), depending on the unit price, ***P<sub>t</sub>*** (e.g., $/m<sup>3</sup>), as follows:

<table><tbody><tr class="odd"><td><span class="math display"><em>w</em><sub>kt</sub> = <em>D</em>(<em>P</em><sub><em>t</em></sub>, <em>x</em><sub>tk</sub>)</span></td><td>Eq. 6</td></tr></tbody></table>

> Where:
>
> ***x<sub>tk</sub>*** is the vector of household characteristics affecting water demand and willingness to pay (WTP) (e.g., income, household size, the existence of a connection to a sewer network)

Rather than a fixed amount, the quantity demanded from an economic perspective varies with respect to price (i.e., higher price entails lower quantity demanded).

In addition to representing the quantity demanded at each price, the demand curve also defines the economic benefits of water received at the point of use. In particular, it represents the maximum amount that households are willing and able to pay for each incremental unit of water. This “marginal” WTP typically decreases with each incremental unit.

Therefore, for individual households, the benefit of water is calculated as the integral under their economic demand curves for water, which can be calculated by:

<table><tbody><tr class="odd"><td><span class="math display"><em>b</em><sub>wtk</sub>(<em>w</em><sub>kt</sub>) = ∫<sub></sub><sup></sup><em>P</em><sub><em>t</em></sub>(<em>w</em><sub>tk</sub>,<em>x</em><sub>tk</sub>)<em>d</em><em>w</em><sub>tk</sub></span></td><td><blockquote><p>Eq. 7</p></blockquote></td></tr></tbody></table>

> Where:
>
> ***b<sub>wtk</sub>*** are the benefits (in monetary terms) to household ***k*** in period ***t*** for a change in water consumption *(**w<sub>kt</sub>**).*
>
> ***P<sub>t</sub>* (w,x)** is the function representing the household’s maximum marginal WTP for water (inverse of the water demand curve)

To specifically estimate the benefits of *publicly supplied* water to households, it is also important to consider the costs to households from receiving water from other sources. Eq. 6 and Eq. 7 represent households’ water demand and benefits from *all* available sources. In effect, the cost of water from other sources acts as an upper bound on households’ WTP (economic benefit) for publicly supplied water.

#### Linear Water Demand Curve

In a simple case with linear demand, the household demand and corresponding WTP function (dropping the k subscript for simplicity) would be:

<table><tbody><tr class="odd"><td><p><span class="math display"><em>w</em><sub><em>t</em></sub> = <em>a</em> + <em>b</em><em>P</em><sub><em>t</em></sub> + <em>c</em><em>x</em><sub><em>t</em></sub></span></p><p><span class="math display">$$P_{t} = \frac{w_{t} - \left( a + cx_{t} \right)}{b}$$</span></p></td><td><blockquote><p>Eq. 8</p><p>Eq. 9</p></blockquote></td></tr></tbody></table>

where ***a***, ***b***, and ***c*** are preference parameters that could, for example, be estimated using regression analysis. In this linear case, the benefits to a household of gaining access to the public water supply system are represented in figure below:

<img src="img\media\image94.png" style="width:4.86458in;height:3.32292in" />

In situations where households lack or have insufficient access to a public water distribution system, it is assumed that the household can pay a price of ***p<sub>t,0</sub>*** for water from alternative sources, such as private vendors (including the economic cost for fetching/buying/storing water). If water is only available at this price, then the demand curve implies that a household would consume ***w<sub>t,0</sub>*** per period ***t***.

With access to the public water distribution system, if the price per unit of water through the public system is ***P<sub>t,1</sub>***<sub>,</sub> then the household’s water demand during period ***t*** would be ***w<sub>t,1</sub>***. The amount of water available to the household from the public system (***w<sub>t,2</sub>***) could be less, equal, or greater than ***w<sub>t,1</sub>***, and the benefits will be calculated as a function of the water available as follows:

-   If ***w<sub>t,2</sub> ≤ w<sub>t,0</sub>**<sub>,</sub>* then the household’s benefit is the avoided expenditure on water from the other source.

<table><tbody><tr class="odd"><td><span class="math display"><em>b</em><sub><em>t</em></sub> = <em>w</em><sub><em>t</em>, 2</sub> * <em>P</em><sub><em>t</em>, 0</sub></span></td><td>Eq. 10</td></tr></tbody></table>

-   If ***w<sub>t,1</sub> &gt; w<sub>t,2</sub>&gt; w<sub>t,0</sub>***, then the household’s benefit is the sum of areas A, B, and C shown in the figure above, where A is the avoided expenditure on water from the other source and B+C is the gross benefit of the difference between *w<sub>t,2</sub>* and *w<sub>t,0</sub>*.

<table><tbody><tr class="odd"><td><span class="math display">$$b_{t} = \left( w_{t,0}*P_{t,0} \right) + \left\lbrack \left( P_{t,0} - \left( \frac{w_{t,2} - \left( a + cx_{t} \right)}{b} \right) \right)*\left( \frac{w_{t,2} - w_{t,0}}{2} \right) \right\rbrack + \left\lbrack \left( w_{t,2} - w_{t,0} \right)*\left( \frac{w_{t,2} - \left( a + cx_{t} \right)}{b} \right) \right\rbrack$$</span></td><td>Eq. 11</td></tr></tbody></table>

-   If ***w<sub>t,2</sub>*&gt; *w<sub>t,1,</sub>*** then the household will consume ***w<sub>t,1</sub>*** (the amount demanded at ***P<sub>t,1</sub>***) and the benefit can be expressed as:

<table><tbody><tr class="odd"><td><span class="math display">$$b_{t} = \left( w_{t,0}*P_{t,0} \right) + \left\lbrack \left( P_{t,0} - P_{t,1} \right)*\left( \frac{w_{t,1} - w_{t,0}}{2} \right) \right\rbrack + \left\lbrack \left( w_{t,1} - w_{t,0} \right)*\left( P_{t,1} \right) \right\rbrack$$</span></td><td>Eq. 12</td></tr></tbody></table>

In each case, the ***net*** benefit of public water supply to the household, ***nb<sub>t</sub>***, can then be calculated by deducting the variable delivery costs of supplying water to the household. Variable costs refer to those costs, such as pumping costs, that depend directly on the quantity of water supplied.

nb<sub>*t*</sub> = *b*<sub>*t*</sub> − (**c** \* *w*<sub>*t*</sub>)

where ***c*** is the average per-unit water delivery cost ($/m<sup>3</sup>).

The ***aggregate* net** benefit of water supplies can therefore be estimated by summing household-level net benefits across all affected households. It can be represented as:

<table><tbody><tr class="odd"><td><span class="math display">$$\text{NB}_{\text{wt}} = \sum_{k = 0}^{K}{\text{nb}_{w_{t_{k}}}\left( {w_{t_{k}}}_{} \right)}$$</span></td><td>Eq. 13</td></tr></tbody></table>

Where:

***K*** is the total of households

#### Hyperbolic Water Demand Curve

An alternative simple form for the demand curve, which is implemented in the WaterALLOC economic module, is a hyperbolic demand equation. In the same way as described above, the benefits can be calculated as the area (integral) under the demand curve for water. In a case with hyperbolic demand, the **aggregate** water demand and corresponding marginal benefit are:

<table><tbody><tr class="odd"><td><blockquote><p>Demand Curve: <span class="math inline"><em>W</em><sub><em>t</em></sub> = <em>α</em><em>P</em><sub><em>t</em></sub><sup><em>β</em></sup></span></p></blockquote><p>Inverse Demand (marginal benefit) curve: <span class="math inline">$P_{t} = \left( \frac{W_{t}}{\alpha} \right)^{1/\beta}$</span></p></td><td><p>Eq. 14</p><p>Eq. 15</p></td></tr></tbody></table>

Where:

> ***W<sub>t</sub>*** is the quantity of water demanded/consumed by all households in period ***t**.*
>
> ***P<sub>t</sub>*** is the price per unit (m<sup>3</sup>) of water in period ***t**.*
>
> ***α*** and ***β*** are coefficients of the aggregate demand function, and ***β*** represents the price elasticity of water demand.[1]

The figure below shows the hyperbolic demand curve with the areas to calculate the benefits for the different supply scenarios (above).

<img src="img\media\image95.png" style="width:5.58333in;height:3.86458in" />

[1] If all households are assumed to have the same household-level demand curve, the aggregate demand is simply the household demand multiplied by the number of households. This also implies that the α parameter for the aggregate demand curve is equal to the α parameter for the household demand curve multiplied by the number of households **K**.

In this case, if, for example, the amount of public water available to households is increased from **W<sub>t,0</sub>** to***W<sub>t,</sub>*<sub>2</sub>**<sub>,</sub> the **aggregate** benefit, ***B<sub>t</sub>**<sub>,\ </sub>*is calculated as the integral of the demand curve (i.e., Area B + Area C).[2]

<table><tbody><tr class="odd"><td><span class="math display"> $$B_{t} = Area\ B + Area\ C = \ \left. \ \left\lbrack \left( \frac{1}{\alpha} \right)^{1/\beta}*\left( \frac{1}{1 + 1/\beta} \right)W_{i}^{1 + 1/\beta} \right\rbrack\  \right|_{W_{t,0}}^{W_{t,2}}$$</span></td><td>Eq. 16</td></tr></tbody></table>

[2] In the unique case where ***β*** equals -1, this equation is undefined, but the benefit calculation simplifies to

<table><tbody><tr class="odd"><td><span class="math display"><em>B</em><sub><em>t</em></sub> =  [<em>α</em>*<em>l</em><em>n</em>(<em>w</em><sub><em>t</em></sub>)] |<sub><em>w</em><sub><em>t</em>, 0</sub></sub><sup><em>w</em><sub><em>t</em>, 2</sub></sup></span></td><td>Eq. 15-1</td></tr></tbody></table>

To estimate the **aggregate *net*** benefit of the change in public water supply, the costs of the additional water supplied must be deducted. This can be done using the average per-unit cost as follows:

<table><tbody><tr class="odd"><td><span class="math display">NB<sub><em>t</em></sub> = <em>B</em><sub><em>t</em></sub> − (<strong>c</strong> * [<em>W</em><sub><em>t</em>2</sub> − <em>W</em><sub><em>t</em>0</sub>])</span></td><td>Eq. 17</td></tr></tbody></table>

#### User Inputs in WaterALLOC

The user inputs to evaluate aggregate benefits of public water supply include:

-   Demand curve parameters (***β*** and ***α*** or ***P<sub>t,1</sub>***)

-   Alternative supply price (***P<sub>t,0</sub>***).

-   Estimating net benefits requires an estimate of the average per-unit cost ***c***.

In addition, for each node, the user can include cost components for water projects that will affect the supply or demand for water in the municipal sector. As with agricultural projects, the user can specify 1) the “capital cost,” representing the one-time costs incurred in the initial stage of a project, and 2) O&M costs representing the ongoing costs incurred annually for the life of the project. O&M costs can be defined either as fixed annual monetary value or as a percentage of the capital costs.

<img src="img\media\image96.png" style="width:6.5in;height:3.82639in" />

### Hydropower Sector

For hydropower projects, the net benefits in each time step is a function of the electricity generated minus the O&M costs. The amount of electric power generated (***Pw<sub>t</sub>***) in period ***t*** in watts, is calculated as follows:

<table><tbody><tr class="odd"><td><span class="math display">Pw<sub><em>t</em></sub> = <em>H</em><sub><em>t</em></sub>* <em>q</em><sub><em>t</em></sub> * <em>η</em>* <em>γ</em></span></td><td>Eq. 18</td></tr></tbody></table>

Where:

> ***H<sub>t</sub>*** is the average head in meters (vertical distance from water level behind dam to turbines) in period ***t***.
>
> ***q<sub>t</sub>*** is the water flow (m<sup>3</sup>/s) through the turbines in period ***t***.
>
> ***η*** is the generator efficiency.
>
> **γ** is specific weight of water (9.807 kN/m<sup>3</sup> @ 5˚C) .

The energy generated (***E<sub>t</sub>***) in period ***t*** in watt-hours (or kilowatt-hours) is the product of electric power times the number of hours generated. The benefit of the hydropower produced (***B<sub>ht</sub>***) can be estimated by:

<table><tbody><tr class="odd"><td><span class="math display"><em>B</em><sub>ht</sub>= <em>P</em><sub><em>t</em></sub> * <em>E</em><sub><em>t</em></sub></span></td><td>Eq. 19</td></tr></tbody></table>

Where:

> ***P<sub>t</sub>*** is the average price or marginal value of the electricity produced in period ***t***.

WaterALLOC uses the MODSIM hydropower simulation tool to estimate the power produced by a project based on the average head simulated in the reservoir in each time step, the average flow released, and physical hydraulic capacity through the turbines as a function of the head. The storage and release relationship in the MODSIM solution is driven by system simulated operations for water supply and storage operations, including supplemental water supply and flood control.

### Cost-benefit Analysis

The net benefits of water allocation are calculated for each MODSIM node (i.e., demand and reservoir) with economic parameters inputs at run time. For agricultural nodes, the net benefit is calculated for every calendar year, while for the domestic water nodes is calculated every month, and for hydropower is computed every time step. The simulation results include a time series of benefits in monetary terms at these intervals.

With these aggregate net benefit estimates for specified water allocations, the Hydro-economic module can be used to assess incremental or marginal benefits between multiple scenarios. Looking at the change in net benefits between runs, we can analyze tradeoffs and compare the performance of scenarios.

In addition, the results for each node include the option for a time series of project costs on an annual basis. The capital costs are assumed to occur at the beginning of the simulation period and the O&M costs occur each year thereafter for the lifespan of the project, which is assumed to be longer than the simulation period.

To support cost–benefit analysis, the model allows the user to compare the project costs and net benefits with the associated water allocation in three different ways: 1) as present values, discounting the future values in the time series with a user-specified discount rate, 2) as annualized values, and 3) as the total simulated, as the sum of the annual values simulated for each node. A benefit-cost ratio and the net benefit-cost present value are used to compare the assumed benefits and costs, with ratio values greater than one indicating larger benefits than costs.

RTI built a dashboard in WaterALLOC to summarize the benefits and cost results per node and water use type and compare the economic analysis results between multiple scenarios. The figure below shows the dashboard with the main analysis areas and user options. The results displayed in the dashboard include the benefits and cost for the base scenario and each scenario selected, which is displayed in the summary type selected, and a table with the incremental economic benefit between the base scenario and the selected scenarios. The dashboard also includes a graph of each demand node cost–benefit per scenario. The cost–benefit ratio (i.e., BC Ratio) is calculated for each row in the tables, when data are available and adequate for the calculation.

<img src="img\media\image97.png" style="width:6.39797in;height:4.63542in" />

## GSFLOW Extension

This extension contains tools to create the MODSIM network for GSFLOW-MODSIM coupled simulation. The main function of these tools is to create a MODSIM network based on the GSFLOW-SFR network. It relies on a shapefile that is created by the Python data processing scripts. The shapefile includes attributes that contain information of the connectivity used by the SFR to move water and is required to link the SFR reaches with the MODSIM links.

The SFR network can contain diversion segments and lakes. Diversion segment could have multiple segments representing different uses or diversion conditions. Flags for storage and non-agricultural use could be set for each of the diversion segments in the shapefile attributes and transferred to the MODSIM links. The SFR shapefile fields include:

<table><thead><tr class="header"><th>Type</th><th>Field</th><th>Description</th></tr></thead><tbody><tr class="odd"><td>Required</td><td>ISEG</td><td>This field contains the SFR segment number. The segment number is added to the MODSIM link description (“ISEG_###|”) and the number is added to the end of the link name.</td></tr><tr class="even"><td></td><td>IOUTSEG</td><td>Segment number downstream of the current segment</td></tr><tr class="odd"><td></td><td>IUPSEG</td><td>This is used to identify diversions. It corresponds to the number of the segments from which the diversion is taken. This number is used to identify the demand node where the diversion segments connect to – when no <em><strong>Demand ID</strong></em> is specified.</td></tr><tr class="even"><td>Optional</td><td>Demand ID</td><td>This is an identifier that groups the diversion segments that serve the same place of use.</td></tr><tr class="odd"><td></td><td>Storage Flag</td><td>This fields contains an ON/OFF flag that indicates if the diversion has a storage facility to store water diverted in the segment before it is provided to the demand. This field is passed to the description of the MODSIM link representing the diversion segment with the <em><strong>STO:</strong></em> prefix.</td></tr><tr class="even"><td></td><td>Non-Agricultural</td><td>This fields contains an ON/OFF flag that indicates if the diversion serves a non-agricultural type of demand. The value in this field is stored to the description of the MODSIM link representing the diversion segment with the “<em><strong>NONAG:”</strong></em> prefix.</td></tr></tbody></table>

### Accessing the Tool

The tool is available in the GSFLOW menu item, when the GSFLOW extension is enabled. The Generate Network item launches the user interface to create the MODSIM network from the SFR shapefile.

<img src="img\media\image98.png" style="width:6.15625in;height:0.78125in" />

The SFR shapefile should be selected in the configuration setting as the scenario Flowline Layer

<img src="img\media\image99.png" style="width:5.90694in;height:1.46875in" />

The user dialog to map the SFR fields to the information required for generating the MODSIM network provides the names of the key information and the corresponding field in the shapefile (Flowline Layer).

<img src="img\media\image101.png" style="width:4.44854in;height:4.32352in" />

The field names can be edited, selecting the field that would like to be edited, and changing the field name in the dropdown box that shows the available fields.

<img src="img\media\image102.png" style="width:4.22917in;height:2.98958in" />

### Expected Outcome

The process creates a new MODSIM network for the active scenario. All the nodes and links in the MODSIM network will be deleted and new links and nodes will be created from the SFR shapefile. The SFR segments in the shapefile are used to create MODSIM links.

#### Diversions

Since water is diverted from the bottom of the SFR segment, the processing of diversions, creates new nodes at the last part (i.e., last part of the line) of the shapefile line to implement the diversion link, assuring that only water in the segment is available for diversion in MODSIM. The diversion node is named “\#\#\#\_DWS”, using the number of the segment for which the downstream node was created.

Each diversion is created with at least one non-storage node to represent the diversion from the source, i.e., Diversion Inflow Node, that is located at the end of the shapefile line used for the diversion segment.

***Demand ID defined***: A diversion inflow node and a demand node are created for each *Demand ID* at the diversion location. The segments associated with that demand are created between the diversion inflow node and the corresponding demand, forming multi-links if multiple segments are associated with the *Demand ID*. The diversion inflow node is named with “*Diversion ID**Diversion***” and the demand is given the *Demand ID* name.

<img src="img\media\image106.png" style="width:4.42708in;height:3.43518in" />

***Demand ID not defined***: a single demand with the name of the IUPSEG is created in this case. All the diversion segments at the current diversion location are implemented between the diversion Inflow node and the demand – a multi-link construct. The name of the demand name is “***DEM\_**IUPSEG\#*”, and the name of the diversion inflow node is “***DEM\_**IUPSEG\#**Diversion***“.

<img src="img\media\image107.png" style="width:4.11458in;height:3.3931in" />

#### Reservoirs (Lakes)

The python processed shapefile includes connectivity through out the lakes for creating the MODSIM network. In general, negative numbers on the OUTSEG indicates the segment is draining to a lake and the number is associated with the lake number. WaterALLOC creates reservoirs at these locations using the shapefile lines to connect the incoming segments to the MODSIM node and the outgoing segments with the segments downstream of the reservoir.

## Operation Optimization Module

-   Provide intro to this module and general capabilities. Place holder for now.

# Scenarios Management

-   Allows set of multiple scenarios for “what if” simulations.

    -   Variables that are associated with scenarios

        -   MODSIM file

        -   HydroBID Settings file

        -   Flow Line Layer

-   Describe the new scenario options

    -   Independent with no data

    -   Independent with snapshot of the seed

    -   Dependent of the seed

> Note: The *Flow Line Layer* for the new scenario is selected based on the MODISM file base scenario.

# Output Visualization

-   Explain the different options to explore results (graphs and tables). Provide link to MODSIM documentation.

-   Explain the option to compare measured vs. simulated flows and statistical metrics to calibrate the models.

-   All MODSIM simulation output is stored in MS Access \*.mdb files, which can be directly opened by users if desired. However, MODSIM provides the capability of spatial selection of node and link objects for convenient graphical output display. After a MODSIM run is successfully executed, *right-button mouse click* on any node or link opens the context menu shown in Fig. 56, but with an added item: *Graph*, which allows rapid display of output results. Any number of additional nodes or links can be selected, providing comparative display of output results for several MODSIM objects on the same

# References

Allen, R.G., Pereira, L.S., Raes, D., and Smith, M., 1998. Crop evapotranspiration-Guidelines for computing crop water requirements-FAO Irrigation and drainage paper 56. FAO, Rome, 300(9), p. D05109.

Allen, R.G., and Pruitt, W.O., 1986. Rational use of the FAO Blaney-Criddle formula. *Journal of Irrigation and Drainage Engineering*, *112*(2), 139–155.

Rineer, J., Bruhn, M. 2013. Technical Note 1. An Analytical Hydrology Dataset for Latin America and the Caribbean. RTI International. Research Triangle Park, NC.

Steduto, P., Hsiao, T.C., Fereres, E. and Raes, D., 2012. *Crop Yield Response to Water* (Vol. 1028). Rome: FAO.

# Help & FAQ

Visit the discussion forum at https://github.com/etrianaGIT/WaterALLOC/discussions

# Contact US

RTI - Center for Water Resources 

https://www.rti.org/focus-area/wateralloc

Dr. Enrique Triana (etriana@rti.org)



