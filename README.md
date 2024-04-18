# Projet de test de réplication de Mariadb


```
# db_master
GRANT REPLICATION SLAVE ON *.* TO repl@'%' IDENTIFIED BY 'slavepass'
```

```
SHOW MASTER STATUS;

mysql: [Warning] Using a password on the command line interface can be insecure.
*************************** 1. row ***************************
File: mysqld-bin.000004
Position: 310
Binlog_Do_DB:
Binlog_Ignore_DB:
Executed_Gtid_Set:
```

```
#db_slave
change master to master_host="mysql",master_user="repl",master_password="slavepass",master_log_file="mysqld-bin.000004",master_log_pos=310;

START SLAVE;

SHOW SLAVE STATUS;
```



## Documentation 

https://www.it-connect.fr/replication-en-temps-reel-masterslave-mysql%ef%bb%bf/

https://mariadb.com/kb/en/changing-a-replica-to-become-the-primary/


https://woshub.com/configure-mariadb-replication/ 

```
When you configure replication for the existing MariaDB database, you must put the database to the read-only mode prior starting the replication in order bin_log number not to be updated.
SET GLOBAL read_only = ON;

You must also create the database memory dump and use it for initial upload of data to MariaDB on your slave server.
```

https://www.digitalocean.com/community/tutorials/how-to-set-up-replication-in-mysql