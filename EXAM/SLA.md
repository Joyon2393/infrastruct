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

## Recovery Point Objective
The maximum timeframe of lost data in the event of a disaster is 1 day, considering that backups are taken only daily.

## Recovery Time Objective
The maximum tolerable downtime for services is 2 hours for extreme cases, although we aim to restore services and data from backup in maximum 1 hour.

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
