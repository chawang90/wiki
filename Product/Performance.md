# Performance

This document outlines techniques we're using to keep the Josephine app fast.

## Database Indexes

The [lol_dba](https://github.com/plentz/lol_dba) gem is a small package of rake tasks that scan your application models and displays a list of columns that probably should be indexed.

```
rake db:find_indexes
```

## Query Count

The [sql_queries_count](https://github.com/comboy/sql_queries_count) rails plugin adds a count of SQL queries per request to your log. So instead of:

```
Completed 200 OK in 249ms (Views: 141.8ms | ActiveRecord: 9.6ms)
```

you will get:

```
Completed 200 OK in 249ms (Views: 141.8ms | ActiveRecord: 9.6ms | SQL count: 9)
```

You can easily look for these by running:
```bash
tail -f log/development.log | grep "SQL count"
```

## N+1 Queries

The [Bullet](https://github.com/flyerhzm/bullet) gem is designed to help you increase your application's performance by reducing the number of queries it makes. It will watch your queries while you develop your application and notify you when you should add eager loading ([N+1 queries](https://secure.phabricator.com/book/phabcontrib/article/n_plus_one/)), when you're using eager loading that isn't necessary and when you should use counter cache.

By default, Bullet emits log messages in development to help you optimize queries. To configure Bullet's logging to be more aggressive, see [bullet#configuration](https://github.com/flyerhzm/bullet#configuration).
