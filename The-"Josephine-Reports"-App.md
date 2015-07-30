Josephine Reports
==================

We have a copy of the production database as a Heroku app called `josephine-reports`. We only use the database, and it only costs us $9 / month.

Access
------

You can access the database here:

```
postgres://obdetgefhasynt:BocF6d7B00rnaDzSiW2QDBvfhI@ec2-54-235-134-128.compute-1.amazonaws.com:5432/d3pr6sq5o2dr7t
```

Updating The Data
-----------------

You can give the reports database fresh data by being all like:

```
heroku pg:backups restore `heroku pg:backups public-url -r production` DATABASE_URL -r reports
```

Yo, idiot!
---------

This uses real user data! So please be careful with it.