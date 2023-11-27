stone-payments.redis
============
Role for Ansible which manages Redis in a standalone setup or cluster

# Quickstart
There's absolute no variable needed to setup a basic, passwordless,
loopback-only, standalone Redis setup. Just include it in a play:
```
- name: install redis
  hosts: all
  roles: stone-payments.redis
```

# Cluster setup
In order to build a cluster, you need to inform the master that he is a
master, and a replica on which master to connect to. You can do all this with
the following excerpt:
```
- name: install redis cluster
  host: all
  roles: stone-payments.redis
  vars:
    redis_srv_conn_bind: "0.0.0.0"
    redis_srv_repl_masterAddr: "1.2.3.4"
    redis_srv_repl_isMaster: "{{ true if redis_srv_repl_masterAddr in ansible_all_ipv4_addresses else false }}"
    redis_sent_enabled: true
    redis_sent_monitors:
      - name: "someMasterName"
        host: "{{ redis_srv_repl_masterAddr }}"
        port: 6379
        quorum: 2
        auth_pass: ""
        down_after_milliseconds: 3000
```

# Other configs
I believe almost every other config is self-explanatory or directly related to
a Redis core feature. Simply override the configs on `defaults/main.yml` and
they will be (hopefully) applied to your system.
