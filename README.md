# INSTALLATION
```shell
$ wget https://github.com/darold/pgbadger/archive/v11.5.tar.gz
$ tar xzf v11.5.tar.gz
$ cd pgbadger-11.5
$ perl Makefile.PL
$ make && sudo make install
```

# POSTGRESQL CONFIGURATION


### You must enable and set some configuration directives in your postgresql.conf before starting.
```shell
$ sudo vim /etc/postgresql/12/main/postgresql.conf
```

``` log_min_duration_statement = 0
    log_line_prefix = '%t [%p]: user=%u,db=%d,app=%a,client=%h '
    log_checkpoints = on
    log_connections = on
    log_disconnections = on
    log_lock_waits = on
    log_temp_files = 0
    log_autovacuum_min_duration = 0
    log_error_verbosity = default
```

```shell
$ sudo systemctl restart postgresql
````

# Build Report
```shell
$ pgbadger -I -q /var/log/postgresql/postgresql-12-main.log  -O /tmp/pg_reports
```

# INCREMENTAL REPORTS
### For example, if you run pgBadger as follows based on a daily rotated file:
```
0 4 * * * /usr/bin/pgbadger -I -q /var/log/postgresql/postgresql.log.1 -O /var/www/pg_reports/
```
[More Details About pgbadger](https://github.com/darold/pgbadger)
