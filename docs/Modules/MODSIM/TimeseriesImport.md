# Time Series
## Time Series Import
    MODSIM -> Import MODSIM Timeseries
This tool allows importing time series stored in a csv file. The headers format allow flexibility in importing different time series types in different units.
### File Format
The file should have the first row with:

    Start Date, End Date, Object Names ....

    This first row is used to find the MODSIM objects, i.e., links or nodes. The name should match the name in the model. 

### Notes
* Dates should start at the data start date
* Missing values should be filled with 0 or -999 for missing measured values 

>[!NOTE]
> Information the user should notice even if skimming.

:::row:::
   :::column span="":::
      Content...
   :::column-end:::
   :::column span="":::
      More content...
   :::column-end:::
:::row-end:::