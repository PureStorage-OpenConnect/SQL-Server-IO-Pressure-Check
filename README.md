# SQL-Server-IO-Pressure-Check
This GitHub repository contains a perfmon data collector template for determining whether a SQL Server instance is experiencing IO related pressure. For anyone familiar with Oracle Automartic Workload Reports (AWR), this provides the means of rendering a similar type of report, but for SQL Server.

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

In addition to the counters above, data for the following SQL Server specific counters should also be collected, note that these are prefixed by the name of the SQL Server instance that is the target of perfmon statistics capture exercise:

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

### 1. Import the Perfmon Data Collector Template

The following walk through illustrates how the perfmon data collector can be used:

1. Download the SQL-Server-IO-Pressure-Check.xml file onto the server running the SQL Server instance that is the target for analysis.

2. Bring up perfmon, the fastest way to do this is to bring up the run prompt and enter perfmon.

3. In the left hand pane in perfmon, expand "Data collector sets", right click "User defined" and select 'New' then "Data Collector Set"

![capture](https://user-images.githubusercontent.com/15145995/53408754-3d320f00-39b7-11e9-84a5-4d95680e259b.PNG)

4. Change the name of the collector from "New Data Collector Set" to something more meaningful, leave the radio button on "Create from template (Recommended)" and then hit 'Next':

![image](https://user-images.githubusercontent.com/15145995/53409059-ef69d680-39b7-11e9-9dd1-e8e7eb5093a5.png)

5. Click on the browse button and navigate to the location of the SQL-Server-IO-Pressure-Check.xml file:

![image](https://user-images.githubusercontent.com/15145995/53409252-5c7d6c00-39b8-11e9-9140-4ad5984e5238.png)

6. Double click on the file and then hit 'Finish':

![image](https://user-images.githubusercontent.com/15145995/53409334-98b0cc80-39b8-11e9-85d8-56f524e27101.png)

7. Double click on the Data Collector Set that has been imported (in the right hand pane) and add the SQL Server specific performance counters listed earlier. Note that the ones added needed to be prefixed by the name of the SQL Server instance that is the target of the perfmon counter data capture.

### 2. Running the Perfmon Data Collector Template

1. The perfmon data collector set can be instigated to capture data in one of two ways:

- Right click on the data collector and select 'Start':

![image](https://user-images.githubusercontent.com/15145995/53409610-42905900-39b9-11e9-8b18-dd767f93678c.png)

- Right click on the data collector and select 'Properties' and then add a schedule to the schedule tab:

![image](https://user-images.githubusercontent.com/15145995/53409685-7cf9f600-39b9-11e9-9c94-ff9d21336626.png)

It is critical that data collection takes place during a time windows when the SQL Server instance is processing a workload which is suspected to be impacted by poor storage performance.

2. Data collection can be stopped by right clicking on the data collector and selecting stop or letting data collection naturally stop when the end of the schedule is reached.

### 3. Generate a PAL Report From The Data Collector .BLG File

1. The perfmon data resides in a .BLG file:

![image](https://user-images.githubusercontent.com/15145995/53409954-4e304f80-39ba-11e9-9775-39ebd1cf47b6.png)

2. Copy the .BLG file to a laptop or PC running Windows.

3. To view the information collected by the Data Collector Set, install PAL (Performance-Analysis-for-Logs) using the .msi in this GitHub [repo](https://github.com/clinthuffman/PAL).

4. Start the PAL tool, the windows app for this is simply called 'PAL'.

5. Go to the "Counter Log" tab, hit browse and navigate to the location of the .BLG file:

![image](https://user-images.githubusercontent.com/15145995/53410353-7f5d4f80-39bb-11e9-9496-edf9f2b18996.png)

6. Hit next, and from the 'Title' pull down list of values select the version of SQL Server that corresponds to the version of the instance the data collector set data was captured for, use "Microsoft SQL Server 2014" for versions 2014 and above, and then hit 'Next':

![image](https://user-images.githubusercontent.com/15145995/53415212-86d72580-39c8-11e9-9da9-8e167b846b6d.png)

7. On the questions tab provide values for the following questions:

- `BPEHealth`      leave the answer to this set to its default

- `OLTPvsOLAP`     if the instance is processing OLTP workloads, select 'True' otherwise select 'False'

- `OS`             the operating system hosting the SQL Server instance

- `PhysicalMemory` the amount of physical memory in the server

- `PLEHealth`      set this to (SQL Server max memory / 4) * 300

- `UsingInMem`     set this to 'True' if memory optimized tables are in use, otherwise set it to 'False'

8. Navigate to the 'Reports' tab, this allows the name format and location of the html files that PAL generates to be changed, change these as required, otherwise leave them as they are.

9. Navigate to the 'Execute' tab and hit finish in order for PAL to analyze the .BLG file and generate a report file.

### 4. Analyze The Contents of The PAL Report











