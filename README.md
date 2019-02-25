# SQL-Server-IO-Pressure-Check
A perfmon data collector template for determining whether a SQL Server instance is experiencing IO related pressure. This data collector set uses the following perfmon counters:

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
