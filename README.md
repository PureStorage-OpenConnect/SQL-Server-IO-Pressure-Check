# SQL-Server-IO-Pressure-Check
A perfmon data collector template for determining whether a SQL Server instance is experiencing IO related pressure. 

## Trace Collector Overview

This data collector set uses the following perfmon counters:

`LogicalDisk(_Total)\Avg. Disk Bytes/Read`

`LogicalDisk(_Total)\Avg. Disk Bytes`

`LogicalDisk(_Total)\Avg. Disk Bytes`

`LogicalDisk(_Total)\Avg. Disk sec`

`LogicalDisk(_Total)\Avg. Disk sec/Transfer`

`LogicalDisk(_Total)\Avg. Disk sec/Write`

`Processor Information(_Total)\% Processor Time`

`LogicalDisk(_Total)\Disk Read Bytes/sec`

`LogicalDisk(_Total)\Disk Reads/sec`

`LogicalDisk(_Total)\Disk Transfers/sec`

`Processor(*)\% Processor Time`

`System\Processor Queue Length`

In addition to the counters above, the following SQL Server specific counters are added, note that these are prefixed by the name of the SQL Server instance that is the target of perfmon statistics capture: 

`<instance-name>:Buffer Node(000)\Page life expectancy`

`<instance-name>:General Statistics\Logins/sec`

`<instance-name>:Locks(_Total)\Lock Requests/sec`

`<instance-name>:Locks(_Total)\Lock Waits/sec`

`<instance-name>:SQL Statistics\Batch Requests/sec`

`<instance-name>:Transactions\Longest Transaction Running Time`

`<instance-name>:Transactions\Transactions`

`<instance-name>:Wait Statistics(Average wait time (ms))\Lock waits`

`<instance-name>:Wait Statistics(Average wait time (ms))\Log write waits`

`<instance-name>:Wait Statistics(Average wait time (ms))\Page IO latch waits`

`<instance-name>:Wait Statistics(Cumulative wait time (ms) per second)\Lock waits`

`<instance-name>:Wait Statistics(Cumulative wait time (ms) per second)\Log write waits`

`<instance-name>:Wait Statistics(Cumulative wait time (ms) per second)\Page IO latch waits`

`<instance-name>:Wait Statistics(Waits in progress)\Lock waits`

`<instance-name>:Wait Statistics(Waits in progress)\Log write waits`

`<instance-name>:Wait Statistics(Waits in progress)\Page IO latch waits`

`<instance-name>:Wait Statistics(Waits started per second)\Lock waits`

`<instance-name>:Wait Statistics(Waits started per second)\Log write waits`

`<instance-name>:Wait Statistics(Waits started per second)\Page IO latch waits`

## Methodology

The following walkthrough illustrates how the perfmon data collector can be used:

1. Download the SQL-Server-IO-Pressure-Check.xml file onto the server running the SQL Server instance that is the target for analysis.

2. Bring up perfmon, the fasest way to do this is to bring up the run prompt and enter perfmon.

3. In the left hand of perfmon, expand "Data collector sets", right click "User defined" and select 'New' then "Data Collector Set"

![capture](https://user-images.githubusercontent.com/15145995/53408754-3d320f00-39b7-11e9-84a5-4d95680e259b.PNG)

4. Change the name of the collector from "New Data Collector Set" to something more meaningful, leave the radio button on "Create from template (Recommended)" and then hit 'Next':

![image](https://user-images.githubusercontent.com/15145995/53409059-ef69d680-39b7-11e9-9dd1-e8e7eb5093a5.png)

5. Click on the browse button and navigate to the location of the SQL-Server-IO-Pressure-Check.xml file:

![image](https://user-images.githubusercontent.com/15145995/53409252-5c7d6c00-39b8-11e9-9140-4ad5984e5238.png)

6. Double click on the file and then hit 'Finish':









