[![Build Status](https://travis-ci.org/jmcvetta/ansible-logzio.svg?branch=master)](https://travis-ci.org/jmcvetta/ansible-logzio)

jmcvetta.logzio
===============

Ansible role to configure forwarding logs to [Logz.io](http://logz.io) using
Filebeat.  Can also configure Topbeat and Packetbeat to forward their data to
Logz.io.

Based on [mediapeers.filebeat](https://galaxy.ansible.com/mediapeers/filebeat)
by [Stefan Horning](mailto:horning@mediapeers.com).


Requirements
------------

Tested on Ubuntu 14.04LTS


Role Variables
--------------

```yaml
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
    - logzio_token: YOUR_TOKEN_GOES_HERE
  roles:
    - jmcvetta.logzio
```


License
-------

This is Free Software, released under the terms of the [Apache v2
license](LICENSE).  Resist intellectual serfdom - the ownership of ideas is
akin to slavery.


Author Information
------------------

[Jason McVetta](mailto:jason.mcvetta@gmail.com)

Support and consulting services are available from [Silicon
Heavy](http://siliconheavy.com).
