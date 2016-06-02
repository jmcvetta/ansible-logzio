[![Build Status](https://travis-ci.org/jmcvetta/ansible-logzio.svg?branch=master)](https://travis-ci.org/jmcvetta/ansible-logzio)

jmcvetta.logzio
===============

Ansible role to configure forwarding logs to [Logz.io](http://logz.io) using
[Filebeat](https://www.elastic.co/products/beats/filebeat).  Can also configure
[Topbeat](https://www.elastic.co/products/beats/topbeat) and
[Packetbeat](https://www.elastic.co/products/beats/packetbeat) to forward their
data to Logz.io.

Based on [mediapeers.filebeat](https://galaxy.ansible.com/mediapeers/filebeat)
by [Stefan Horning](mailto:horning@mediapeers.com).


Requirements
------------

Tested on Ubuntu 14.04LTS


Role Variables
--------------

```yaml
logzio_token: YOUR_LOGZIO_TOKEN

# Logging level for Filebeat, Topbeat, and Packetbeat daemons
logzio_daemon_log_level: warning


#-------------------------------------------------------------------------------
#
# Logs
#
#-------------------------------------------------------------------------------

# Example, overwrite this variable:
logzio_logs:
  - 
    # Paths for files you want forwarded to Logz.io
    paths:
      - '/var/log/apache2/access.log'
      - '/var/log/apache2/error.log'
    # codec must be 'plain' or 'json'
    codec: plain 
    # Informational tag describing what type of data these files contain
    type: apache2

# Extra logs - will be added to logzio_logs list at runtime.  Facilitates
# having a base set of logs plus extra logs per host or group.
logzio_extra_logs: []

# Ignore files which were modified more then the defined timespan in the past.
# Time strings like 2h (2 hours), 5m (5 minutes) can be used, or the value can 
# be left blank to disablet this option (default).
logzio_ignore_older: 


#-------------------------------------------------------------------------------
#
# Topbeat
#
#-------------------------------------------------------------------------------

# Install and configure Topbeat
logzio_topbeat: false

# In seconds, defines how often to read server statistics
logzio_topbeat_period: 60

# What information should Topbeat monitor?
logzio_topbeat_system: true
logzio_topbeat_process: false
logzio_topbeat_filesystem: true
logzio_topbeat_cpu_per_core: false


#-------------------------------------------------------------------------------
#
# Packetbeat
#
#-------------------------------------------------------------------------------

# Install and configure Packetbeat
logzio_packetbeat: false

# Netowrk interface devices to monitor
logzio_packetbeat_interfaces: any
```

You can also define variable `logzio_extra_prospectors` on a per-host or
per-group basis.  This variable is concatenated with `logzio_prospectors`
when rendering the configuration template.


Dependencies
------------

* [jmcvetta.cfssl-trust](https://galaxy.ansible.com/jmcvetta/cfssl-trust/)


Example Playbook
----------------

```yaml
- name: Ensure logs are forwarded to Logz.io
  hosts: servers
  vars:
    logzio_token: YOUR_TOKEN_GOES_HERE
	logzio_logs:
      - type: fail2ban
	    codec: plain
        paths:
          - /var/log/fail2ban.log
  roles:
    - jmcvetta.logzio
```


License
-------

This is [Free Software](http://www.gnu.org/philosophy/free-sw.en.html),
released under the terms of the [Apache v2 license](LICENSE).  Resist
intellectual serfdom - the ownership of ideas is akin to slavery.


Author Information
------------------

[Jason McVetta](mailto:jason.mcvetta@gmail.com)

Support and consulting services are available from [Silicon
Heavy](http://siliconheavy.com).
