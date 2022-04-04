# Scenarios
Scenarios in WaterALLOC allow organizing the files and data for HydroBID and MODSIM.  
## New Scenarios
A new scenario can be created as a dependent of another scenario or independent with and without snapshot of the data. 
### Data Management 
The data copied when creating a new scenario includes:
#### Hydro-BID
* Create a new folder in the WALLOCFiles folder with the new scenario name to store the new scneario files
* Copy of the seed settings file with the name of the new scenario, copied into the new folder
### MODSIM
* Create a copy of the seed scenario XY file with the name of the new scenario in the same folder where the seed file is located
* When a seed file is used, the seed scenario runoff support data is copied to the new scenario.  This is only performed when a copy of the XY file is created becasue the runoff table relies on the non-storage nodes GUID.

    > IMPORTANT <br>
    > The runoff table only can be used with a network nodes that have the same GUIDs than the network that it was created.
    
### WaterALLOC
* If snapshot of a seed scenario makes a copy of the data stored in the WaterALLOC database asociated with the new scenario (i.e., scenID).  Data copied includes:
    * Demand estimation support data, including agricultural and domestic data for each node.
    * Hydro-economics data for each node.
    * Climate data imported from HydroBID. 