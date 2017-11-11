HAPRoxy & Letsencrypt
=====================

[![Build Status](https://travis-ci.org/pyslackers/ansible-role-haproxy.svg?branch=master)](https://travis-ci.org/pyslackers/ansible-role-common)

Ansible role to install and configure haproxy with letsencrypt certificates.

Role Variables
--------------
* `redirect_http`: Use https and redirect http (default to `false`).
* `default_backends`: Default backend.

* `haproxy_backends`: Dict of backends.
    * `domain`: Domain serving this backends.
    * `letsencrypt`: Generate letsencrypt certificate for `domain` (use `staging` for the staging letsencrypt).
    * `servers`: Dict of servers for this backend (`key`: server name, `value`: domain/ip:port of the server)
* `haproxy_redirects`: Dict of redirections.
    * `domain`: Domain to redirect.
    * `destination`: Destination domain.
    * `letsencrypt`: Generate letsencrypt certificate for `domain` (use `staging` for the staging letsencrypt).

* `certbot_port`: Listening port for certbot during certificates renewal (default to `32456`).
* `haproxy_stats_ip`: Listening IP for haproxy stats (default to `127.0.0.1`).
* `haproxy_stats_port`: Listening port for haproxy stats (default to `8080`).

Example Playbook
----------------

```yml
- hosts: localhost
  vars:
    default_backend: test
    haproxy_backends:
      test:
        domain: test.example.com
        letsencrypt: no
        servers:
          test-01: 127.0.0.1:8000
          test-02: 127.0.0.1:8001
    haproxy_redirects:
      foo:
        domain: foo.example.com
        destination: http://test.example.com
        letsencrypt: no
  roles: 
    - pyslackers.haproxy
```

License
-------

MIT
