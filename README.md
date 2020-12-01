# ansible-role-mysql [![Build Status](https://travis-ci.org/shengyou/ansible-role-mysql.svg?branch=master)](https://travis-ci.org/shengyou/ansible-role-mysql)

=========

安裝 mysql。

適用於
* Ubuntu 14.04, 16.04
* CentOS 6, 7

Ubuntu 14.04 將會安裝 mysql 5.5

Ubuntu 16.04 將會安裝 mysql 5.7

CentOS 則會根據 variable: default_mysql_version 來決定安裝哪一個版本。


Requirements
------------

* ansible >= 2.4
* python >= 2.6

Role Variables
--------------

default variables 如下

```
mysql_password: "DefaultMysqlPassword"
mysql_port: "3306"
default_mysql_version: 57

default_character_set_57: "utf8mb4"
collation_server_57: "utf8mb4_unicode_ci"
init_connect_57: "'SET NAMES utf8mb4'"

default_character_set_56: "utf8"
collation_server_56: "utf8_general_ci"
init_connect_56: "'SET NAMES utf8'"

default_character_set_55: "utf8"
collation_server_55: "utf8_general_ci"
init_connect_55: "'SET NAMES utf8'"
```

Ubuntu 專用的 Variables，因為要將 ulimit 開大才能調高 MySQL 的 max_connections
```
LimitNOFILE: 4510
LimitMEMLOCK: 4510
```

用來設置自訂的 my.cnf，請輸入 source 檔案的路徑。
```
custom_my_cnf:
```

Example Playbook
----------------

```
- name: ansible-role-mysql.yml
  hosts: your_host
  gather_facts: yes
  become: yes

  vars:
    mysql_password: "1234567890$"
    mysql_port: 33060
    custom_my_cnf: "path/to/file"

  roles:
    - ansible-role-mysql
```


License
-------

MIT
