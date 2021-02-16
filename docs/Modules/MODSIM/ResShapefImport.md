# Import Reservoirs from Shapefile

|Input|Requiremient|   |   |   |
|---|---|---|---|---|
|Shapefile|Points with the general location of the reservoir|   |   |   |
|Attributes | - Name <br> - GUID <br> - Reservoir Capacity <br> - Power Capacity <br> - Max. Surface Area <br> - Max Depth <br> 

## User Interface
1. User will be prompted to browse to select the shapefile file 
2. Import User Dialog 
    
    ![Reservoir import user interface](../../img\ImportRes.png)

    The attribute mapping tree allows selecting the shapefile field to import into the different MODSIM attributes.
3. Calibration Strucutures

    |Option|Description|
    |---|---|
    |Set Calibration Structures| Creates calibration structures around the identified gage links. This includes a sink node (Local Losses) and a source at the downstream end
    |Set Sources at Upstream Nodes|It finds non-storage nodes that don't have any links coming in and creates a source structure (Source and sink), connected with a link which names starts with "LocalGains_" + the name of the downstream gage + name of the node connecting to|
    |Map Coordinate factor|This factor is used to set the distance of the calibration structures to the network.|
    


## Algorithm
For each point, the closest node is found based on the straight distance using the x and y coordinates. The nodes which name start with "Calib" are not considered, so that reservoirs are not attached to calibration structures. 

### Connecting the Reservoir Node
There are two options:
1. Closest Node
    
    If the user select the option to connect the reservoir, the reservoir accrual is connected from the closest node and the outflow link to the next downstream node. 
    Exceptions: 
    * If the bypass link is flagged with 'measured' time series
    * if there are no outflow links from the closest node
    
        In these cases the outflow link is connected to the closest and the accrual is connected to the next upstream node.  

2. Defined Node
    
    This option requires the name of the node to be connected specified in a attribute field of the shapefile. 

