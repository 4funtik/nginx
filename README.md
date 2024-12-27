Nginx
=========

Эта роль настраивает Nginx для обслуживания нескольких доменов, работы с самоподписанными сертификатами и управления сертификатами Let's Encrypt. Также роль настраивает конфигурации Nginx, директории и файлы для веб-хостинга, включая автоматическое обновление SSL-сертификатов.

Requirements
------------

Необходима коллекция community.crypto для создания самоподписанных сертификатов и управления SSL-ключами.

Role Variables
--------------

```yaml
nginx_configs: <path>
nginx_letsencrypt_cert_renewal: <true/false>
nginx_letsencrypt_cert:
<- domain>
nginx_selfsigned_cert:
<- domain>
nginx_vhosts:
<- host>
```

`nginx_configs` Путь к директории с шаблонами конфигурации Nginx.

`nginx_letsencrypt_cert_renewal` Логическое значение, которое указывает, следует ли настроить автоматическое обновление сертификатов Let's Encrypt.

`nginx_letsencrypt_cert` Список доменов для настройки сертификатов Let's Encrypt.

`nginx_selfsigned_cert` Список доменов для создания самоподписанных сертификатов.

`nginx_vhosts` Список доменов для настройки виртуальных хостов в Nginx.

Dependencies
------------

Роль не зависит от других ролей.

Example Playbook
----------------
Примеры использования роли с переданными переменными:

```yaml
---
- hosts: devops_2
  roles:
    - nginx
    - user
  vars:
    nginx_configs: "/home/tester/ansible/infra/roles/nginx/templates/for_devops_4/"
    nginx_letsencrypt_cert_renewal: true
    nginx_letsencrypt_cert:
      - 494042593-students.devboxops.xyz
    nginx_selfsigned_cert:
      - 494042593-proxied-students.devboxops.xyz
    nginx_vhosts:
      - 494042593-students.devboxops.xyz
      - 494042593-proxied-students.devboxops.xyz
```


License
-------

BSD

Author Information
------------------

Mikhail Merkushev freeedomall@list.ru
