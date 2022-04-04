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
3. Options

    |Option|Description|
    |---|---|
    |Attribute mapping| Allows the user to select fields from the shapefile to assign attributes for the new nodes.
    |Connections|It finds non-storage nodes that don't have any links coming in and creates a source structure (Source and sink), connected with a link which names starts with "LocalGains_" + the name of the downstream gage + name of the node connecting to|
    |Source Node|This option creates a non-storage nodes connected to the reservoirs nodes to simulate local inflows to the reservoir nodes.|

## Algorithm
For each point in the shapefile a new reservoir node is created with the information mapped in the shapefile.  In the case of the GUID, the MODSIM GUID will be replaced with the value specified in the shapefile. The nodes which name start with "Calib" are not considered, so that reservoirs are not attached to calibration structures. 

### Connecting the Reservoir Node
There are three options:
1. No connection
    This option creates the reservoir node, but does not connect it to the network.  
2. Closest Node
    
    If the user select the option to connect the reservoir, the closest node is found based on the straight distance using the x and y coordinates. the reservoir accrual is connected from the closest node and the outflow link to the next downstream node. 
    Exceptions: 
    * If the bypass link is flagged with 'measured' time series
    * if there are no outflow links from the closest node
    
        In these cases the outflow link is connected to the closest and the accrual is connected to the next upstream node.  

3. Defined Node
    
    This option requires the name of the node to be connected specified in a attribute field of the shapefile. The algorithm creates a single link between the reservoir and the speciifed node to connect the reservoir to the network. 

### Create a Source
This option creates a non-storage node connected to the reservoir to simulate local inflow to the new reservoir node.  This construct creates a non-storage node with 0 inflow and a connected link that is open.  

#### Internal Code Notes
 The source node is located on the same X coordinate than the reservoir node and will add 5 * coordFactor to the Y coordinate. The coordFactor is set to 100 internally.   