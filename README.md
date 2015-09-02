Elasticsaerch Kibana
=========

install and run elasticsaerch and kibana for ec2 or vagrant

set crontab for elasticsaerch-curator

Requirements
------------

Variables
--------------

### stage_vars/{stage}.yml

#### environment

* ec2 or vagrant

#### plugins

```
plugins:
  { plugin_name }:
    repo: { repository path }
```

* default installed plugin
    * mobz/elasticsearch-head
    * royrusso/elasticsearch-HQ
    * lukas-vlcek/bigdesk

#### curator

* Set curator job

```
curator:
  indices:
    {index name prefix}:
      command: {curator subcommand}
      state: {present or absent}
      available_days: { days }
      exec_minute: { minute }
      exec_hour: { hour }
```

* e.g.)

```
curator:
  indices:
    nginx_access:
      command: delete
      state: present
      available_days: 5
      exec_minute: 0
      exec_hour: 4
```

* crontab

```
#Ansible: curator nginx_access indices
0 4 * * * /usr/bin/curator --host 192.168.20.20 delete indices --prefix nginx_access --older-than 5 --time-unit days --timestring \%Y-\%m-\%d
```

### hosts.{stage}.yml

* elasticsaerch_master
    * set master node

* e.g.)

```
node_master=true node_data=false
```

run as master and data node.

```
node_master=true node_data=true
```

* elasticsaerch_data
    * Set data node

Run
------------

```
ansible-playbook -i hosts.{stage} site.yml
```

### Tags

When variables setting includes a change, I attach a tag

* config
    * elasticsaerch
    * nginx
* cron
    * cron

Dependencies
------------

* nginx
* supervisord
* epel

