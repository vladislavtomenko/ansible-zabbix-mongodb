zabbix-mongodb
=========

Ansible role to install scripts for mongodb monitoring in zabbix. Original project: https://github.com/nightw/mikoomi-zabbix-mongodb-monitoring

Requirements
------------

This role requires php, mongo driver for php and git.

Role Variables
--------------

You can see full list of default variables in defaults/main.yml

zabbix_mongodb_centos_packages - additional packages to install. Default: php-devel, php-pecl-mongo <br /> 
zabbix_mongodb_git_repo - url to git project. Default: https://github.com/nightw/mikoomi-zabbix-mongodb-monitoring.git <br /> 
zabbix_mongodb_path - path for git clone. Default: /opt/zabbix-mongodb <br /> 
zabbix_mongodb_git_ref - commit to clone. Default: HEAD <br />
zabbix_mongodb_databases - list of zabbix server. It's an array, every element there is a dictionary. Element variables: <br />
  title - comment in crontab. Default value is based on hostname <br />
  state - state of cron task. Default: present <br />
  user - user to run cron job. Default: root <br />
  interval - interval to check mongodb in minutes. Has cron-like syntax. Default: * <br />
  mongodb_version - version of mongodb server. Available values: 2.2, 2.4, 3.2 . Default : 3.2 <br />
  zabbix_server - address of zabbix server. Default: localhost <br />
  zabbix_port - port of zabbix server. Default: 10051 <br />
  hostname - name of host. Should be the same as agent name in zabbix server. Default value is based on nodename. <br />
  mongodb_address - address of mongodb server <br />
  mongodb_port - port of mongodb server. Default: 27017 <br />
  mongodb_user - mongodb server user. <br />
  mongodb_password - password of mongodb user. <br />
  
  


Dependencies
------------

You can use geerlingguy.git ansible role for git installation.

Example Playbook
----------------

An example of playbook with 1 mongodb server.

    - hosts: servers
      roles:
      - role: vladislavtomenko.zabbix-mongodb
        zabbix_mongodb_databases:
        -
          zabbix_server: localhost
          hostname: mongodb.local
          mongodb_address: 192.168.1.71
          mongodb_user: zabbix
          mongodb_password: zabbix

License
-------

BSD
