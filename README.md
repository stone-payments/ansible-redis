stone-payments.redis
============
Role for Ansible which manages Redis in a standalone setup or cluster

## Requirements

- Ansible version 2.8+ (tested with ansible v2.10.3)
## Role Variables

```yaml
- name: install redis cluster
  host: all
  roles: stone-payments.redis
  vars:
    redis_install_enabled: true
    config_redis_enabled: true
    redis_reboot_allowed: true
    redis_version: 6.2.3
    config_newrelic_enabled: true
    redis_password: "..."
    redis_newrelic_env: "..."
  
The role includes extensive configuration options check [`defaults/main.yml`](default/main.yml).

## Dependencies

None.

## Install

Add the following on your `requirements.yml`:

```yaml
- name: stone-payments.redis
  src: git+git@github.com:stone-payments/ansible-redis.git
  scm: git
  version: "master" # see the git tags for available versions


## Contributing

Just open a PR. We love PRs!

## License

MIT