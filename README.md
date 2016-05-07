Ansible role MariaDB
=========

Installs MariaDB 10.1 on Ubuntu Trusty

Requirements
------------

Ansible and Ubuntu Trusty

Role Variables
--------------

This role contains a large set of variables that controls how the mariadb configuration file looks. All the defaults are listed here:

```yaml
---
mariadb_max_connections: 100
mariadb_connect_timeout: 5
mariadb_wait_timeout: 600
mariadb_max_allowed_packet: 16M
mariadb_sort_buffer_size: 4M
mariadb_bulk_insert_buffer_size: 16M
mariadb_tmp_table_size: 32M
mariadb_max_heap_table_size: 32M # should match Aria-pagecache buffer size!!
mariadb_table_cache: 256
mariadb_open_files_limit: 65535
mariadb_aria_pagecache_buffer_size: 32M 

# innodb general optimizations
mariadb_innodb_log_file_size: 50M
mariadb_innodb_buffer_pool_size: 64M
mariadb_innodb_buffer_pool_instances: 8 #Divide the buffer pool into this many equaliy size slices - should improve concurrency handling greatly, the "high performance mysql book" states that 8 is the magic number to go with
mariadb_innodb_log_buffer_size: 8M
mariadb_innodb_file_per_table: 1
mariadb_innodb_open_files: 400
mariadb_innodb_flush_method: O_DIRECT

# storage optimizations
mariadb_innodb_flush_neighbors: 0
# Recommendation for SSD hardware is 2K => 20K, going with a conservative low value to not overload the disk...
mariadb_innodb_io_capacity: 1500 
mariadb_innodb_read_io_threads: 8
mariadb_innodb_write_io_threads: 8
# Let Innodb control the thread concurrency and query ticket numbers.
mariadb_innodb_thread_concurrency: 0 

mariadb_bind_address: 127.0.0.1 
```

Most likely the `mariadb_bind_address` should be updated. For performance loptimizations look into changing `mariadb_innodb_io_capacity` and `mariadb_innodb_buffer_pool_size`.
 
Dependencies
------------

No dependencies 

Example Playbook
----------------

You can use the role like this

```yaml

- hosts: servers
  roles:
      - { role: nover.mariadb }
  vars_files:
      - vars/mariadb.yml

```

Where `vars/mariadb.yml` should contain your variable overrides to fit your needs.

License
-------

GitHub The Unlicense
