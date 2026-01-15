The MySQL slave server stopped replicating the data from the MySQL master server resulted in the Prometheus alert. 
Possible reasons:
Updating the Master / Slave connection
Modifying the MySQL configuration files
 Incorrect use of Bind address/server-id
MySQL slave server down.

These kinds of issues can trigger the Prometheus warning.

mysql_slave_status_slave_io_running == 0    -   There is no data received on the Slave server.
mysql_slave_status_slave_sql_running == 0   -   The MySQL slave server is down. 

If the alert fires, check the MySQL server status and if the server is working the next step has to be checking the connection between the servers. Then the configuration files, and the MySQL slave access has to be checked.


---

The exported Grafana Dashboard contains panels for:
mysql_slave_status_seconds_behind_master
mysql_slave_status_slave_sql_running
mysql_slave_status_slave_sql_running

I have locally created a Master and Slave MySQL server using Vagrant and then exported the Metrics using MySQL Exporter to my locally hosted Prometheus. Added Prometheus to Grafana then created the panels. 

Uploaded both the demo Grafana and the Template dashboard. 







