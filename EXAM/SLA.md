# Backup SLA
- Our infrastracutre's services are all based on databases. 
Therefore, our main backup should be databases as our services highly depend on them.
The following is a summary of our infrastracture architecture:
- Bind is our main DNS server in which our services are configured according to.
- Wordpress works with MySQL.
- Prometheus works with exporters to deliver metrics of our services.
- Telegraf works with Influxdb for syslog logs.
- Grafana has Prometheus and Influxdb as a datasource.

## Coverage: Included Services
- MySQL: Database Dump, will have our wp data.
- InfluxDb: Database Dump.
- Grafana: Database and Configuration (JSON Format).

## Storage
- Backup scheme should follow the 3-2-1 rule.
- two onsite, each in different backup server(s)
- One in a cloud option, or an offsite datacenter.


## Coverage: Excluded Services
- Haproxy: Provisioned with Ansible.
-  Telegraf: everything we need is already in influxdb.
- Prometheus: Provisioned with Ansible along with exporters.
- Bind: Provisioned with Ansible.

## RTO
- 8 hours maximum of downtime is the way to go for our highly available services.

## RPO
- We can only afford 8 hours of RTO, therefore, we should have just 12 hours of RPO to keep data loss at a minimum.

## Frequency
- Full local backups: every night
- Full remote backups: every night
- Incremental backups: Weekdays 

## Versioning
Due to our frequency, different versions of the backups should be present.

## Retention
Backups with a shelf-life of older than 31 days are deemed to be unusable and thus deleted.
 
## Usability
- Verifying the integrity of our backups should be done weekly.
