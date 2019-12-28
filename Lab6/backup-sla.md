# Backup SLA

## Coverage
- SQL: Dumps
- Wordpress: Config:
- Bind9: named.* db.*


## RPO
- Data transfer for all cronscripts will take around 5 minutes.
- MYSQL: As our database grows the time will increase, therefore , the RPO for MySQL in this one should be around 3 hours maximum.
- server clocks are in perfect sync
## RTO
- 5 Hours is the RTO as our infrastracture is tightly coupled together, meaning Wordpress won't work without mysql and losing bind9 means our nameservers won't resolve incurring a configuration error in our infrastracture.
  
## Usability
- Since Duplicity is used, we can unpack the .tar.gz file it creats to extract our files.
- MYSQL: The dump files in .sql format can easily be imported to the MySQL server
- Wordpress: the backed up files originally from /usr/share/wordpress can be moved there again
- DNS: Config files can be restored back to /etc/bind/