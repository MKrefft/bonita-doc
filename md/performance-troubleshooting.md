# Performance troubleshooting

Learn how to monitoring your Bonita Platform and troubleshoot performance issues.


We recommend that you monitor your system regularly, so that if you suspect a performance degradation, you can repeat these checks and identify the potential problem areas by comparing the performance to the normal level. 

When troubleshooting a performance problem, we recommend that you first check your system and network, and then check your Bonita platform and configuration. Follow the order of the topics in this page. 
This will help you identify problems that occur because the actual load on the system exceeds the expected load so the provisioning is not sufficient. They will also help you identify transient problems.

## System

These are the key indicators to check:

* CPU: monitor CPU usage for each hardware platform, and check that it does not exceed 80%
* CPU: check that all available CPUs are used on each hardware platform
* Memory: monitor memory swap, and check that it is not used
* Memory: monitor the amount of memory used
* Disk: monitor disk I/O

Many tools exist in every operating system for system monitoring. For example:

* For Linux: ps, top, iotop, vmstat, iostat, sysstat
* For Windows : tasklist, process monitor, process explorer

These tools can be used in conjunction with monitoring systems such as like Nagios or Zabbix.

Bonita also provides a [PlatformMonitoringAPI](http://documentation.bonitasoft.com/javadoc/api/${varVersion}/index.html) that you can use to obtain some of this information. 

## Network

Network performance has a direct impact on the duration of an instance. We recommend that you measure network performance at the following points: 

* Between the server hosting the Bonita Engine and the database server. Check that the servers ping time duration is less than 1ms. There are many connections between Engine and the database, so network performance between these two servers has huge impact on performance. 
* between the server hosting the Bonita Engine and any other servers used (typically those called by connectors). As connectors are often used to enable Bonita to communicate with outside world, network performance has impact on performance.

## JVM

These are the key indicators to check:

* Memory: heap, memory used by objects
* Threads: Number of threads, number of deadlocks

A large number of deadlocks, or memory heap starvation may indicate a performance issue.
Follow the [JVM performance tuning recommendations](performance-tuning.md) and increase provisioning to get the optimum performance.

Many OpenSource and proprietary tools exist for JVM monitoring. 
These parameters can be obtained through monitoring system like Nagios or Zabbix. You can also retrieve them using the [PlatformMonitoringAPI](http://documentation.bonitasoft.com/javadoc/api/${varVersion}/index.html).

## Database

All databases provide information to monitor the following:

* Connections: monitor the number of connections in parallel
* Transaction: monitor the number of transactions that are committed, and the number that are rolled back
* Memory : Size used by database,
* Disk space used by database

If actual usage reaches the limit of available capacity, this can indicate a performance issue.

These values can be monitored through a monitoring system like Nagios or Zabbix. 
You can also get the number of active transaction using the [MonitoringAPI](http://documentation.bonitasoft.com/javadoc/api/${varVersion}/index.html).

## Bonita Engine connections

Bonita Engine performance is strongly linked by the number of connections. The number of connections from the Bonita Portal directly influences the number of connections to the database through the number of workers, and the number of connector threads.

To avoid overloading the Engine, check that the following connection numbers are coherent:

* Bonita client
* Bonita Engine
* Database

Predict and then monitor the following:

* Users: the total number of users and the maximum number of parallel users
* Processes: the total number of instances of all processes and the maximum number of parallel tasks

All connection numbers must be defined according to the performance tuning recommendations:

* Monitor connection number managed by client (see [Client Threads](performance-tuning.md))
* Check connection number managed by Bonitasoft Server (See [Work Service](performance-tuning.md), Connector service, and [Scheduler Service](performance-tuning.md))
* Check number of database connections defined in Bonitasoft (see [Database connections](performance-tuning.md) and [Datasource settings](performance-tuning.md))
* Check maximum number of simultaneous connections on database
* Monitor number of simultaneous connections on database
* Monitor SQL request duration time

## Connectors

Use the [connector time tracker](performance-tuning.md) to check connector performance. 

## Cron jobs

The Bonita Engine uses the Scheduler service to trigger jobs in a recurrent manner. It might be possible to improve performance by [optimizing the cron settings](performance-tuning.md).

## Performance tuning

See [Performance tuning](performance-tuning.md).
