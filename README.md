## redis

[![Build Status](https://travis-ci.org/Oefenweb/ansible-redis.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-redis) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-redis-blue.svg)](https://galaxy.ansible.com/tersmitten/redis)

Set up the latest stable redis server in Ubuntu systems (using [Chris Lea's ppa](https://launchpad.net/~chris-lea/+archive/ubuntu/redis-server)).

#### Requirements

None

#### Variables

* `redis_instance_name`: [default: `''`]: The name of the redis server instance, required when you want to run multiple instances
* `redis_limit_no_file`: [optional]: Call `ulimit -n` with this argument prior to invoking Redis itself (e.g. `65536`)

A lot (see `defaults/main.yml`)

Some commonly used:

* `redis_port` [default: `6379`]: Accept connections on the specified port
* `redis_bind` [default: `[127.0.0.1]`]: Listen for connections form the specified IP addresses
* `redis_databases` [default: `16`]: The number of databases
* `redis_saves` [default: `[{seconds: 900, changes: 1}, {seconds: 300, changes: 10}, {seconds: 60, changes: 10000}]`]: Will save the DB if both the given number of seconds and the given number of write operations against the DB occurred
* `redis_slaveof` [default: `{masterip: null, masterport: null}`]: Use slaveof to make a Redis instance a copy of another Redis server
* `redis_masterauth` [default: `null`]: Master server password
* `redis_requirepass` [default: `null`]: Require clients to issue `AUTH <PASSWORD>` before processing any other commands
* `redis_maxclients` [default: `null`]: Set the max number of connected clients at the same time
* `redis_maxmemory` [default: `null`]: Don't use more memory than the specified amount of bytes

* `redis_vm_overcommit_memory` [default: `false`]: Whether or not to set system overcommit policy, [see](http://redis.io/topics/faq#background-saving-is-failing-with-a-fork-error-under-linux-even-if-i39ve-a-lot-of-free-ram). Setting it to `1` is probably what you want
* `redis_transparent_hugepage` [default: `false`]: Whether or not to disable transparent huge pages, [see](http://redis.io/topics/latency#redis-latency-problems-troubleshooting). Setting it to `never` is probably what you want

#### Dependencies

None

#### Example(s)

##### Single instance

```yaml
---
- hosts: all
  roles:
    - redis
```

##### Multiple instances

```yaml
---
- hosts: all
  roles:
    - role: redis
      redis_instance_name: 'write-through'
      redis_port: 6380

- hosts: all
  roles:
    - role: redis
      redis_instance_name: 'queue'
      redis_port: 6381
```

**Note** that multiple host sections are needed to flush handlers between role calls.

#### License

BSD

#### Author Information

Mischa ter Smitten (based on work of Benno Joy)

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-redis/issues)!
