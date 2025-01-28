Amazon RDS Overview - 
RDS stands for Relational Database Service.

Its manage DB service for DB use SQL as query lanagua
it allows you to create databased in the cloud that are manage bu aws.

Postgres 
Mysql
MariaDb
Oracle
SQL Server
Aurora (Aws prpriertday Database)



Advanategve over using RDS versus deploying DB on EC2 
RDS is managed Service 
  Automate proviosiong, OS patching 
  Continously backup and restore to spicifc timestamd
  Monitering dashboards.
  Read replicase for imrpvoed read performance 
  multi AZ setup for DR 
  mainiantace windows for upgrade
  scaling capabilyt 
  Storage backed by EBS.
but you can't ssh into your instances.

RDS - Store Auto Scaling 
Helps you increase storge on your RDS Db instance dynamically.
When RDS detects you are running out of free database storage.


user -> application Read/write --------> Amazon RDS ---------> Storage.

Automatically modify storage if : 
 free storage is less then 10 % allocated storage.
 Low staoger lasts at least 5 minutes
 6 hours have passed sinc modification
 Useful for application with unpredicatable workloads.
 support all RDS databse engines.


 RDS Read Replicas for Read scalablity -
Application -> writes reads -> RDS DB Instances.
upto 15 REad replicase withinz AZ cros AZ or cross region 

Replication is ASYNC so ready are eventually consistent.

Replia case can be promoted to theier own DB,.


RDS replicase - use cases.
  You have a production database that is taking on normal load.
  you want to run a reporting application to run some analytics .
  you create a read replica to run the new workload there.
  The production application is unaffected.
  not use insert update delete.
  for only slect.

  RDS Read replicas - Network cost 
  In AWS there's a network cost when dat goes from AZ to another.
  FOr RDS read replicase within the samee region, you dont pay that fee.

Same region no fee but cross region has fee.

RDS multi AZ (Disaster Recoverey) - 
SYNC Replication
One DNS Name - automaticsapp failover to standby,.
increawse availbliyt.
failover in case of loss of AZ loss of network
No manual intervention in apps.
Note - The read replicase be setup as 

