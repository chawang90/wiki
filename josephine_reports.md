# Josephine Reports

We have a copy of the production database as a Heroku app called `josephine-reports`. We only use the database, and it only costs us $9 / month.

## Database Access

You can access the database here:

```yaml
username: obdetgefhasynt
password: BocF6d7B00rnaDzSiW2QDBvfhI
host: ec2-54-235-134-128.compute-1.amazonaws.com
port: 5432
database: d3pr6sq5o2dr7t
```

## AWS Access

We have an AWS instance whose sole purpose in life is to refresh the `josephine-reports` database at scheduled intervals. You'll need Google drive installed, with access to the `Development/Keys` directory.

To connect:

```bash
# This runs the following command.
# ssh -i ~/Google\ Drive/Josephine/Development/Keys/JosephineReportsAWS.pem ec2-user@ec2-54-148-22-107.us-west-2.compute.amazonaws.com
joreports
```

Sha-bam! You should be connected. (Note: you'll need to have Google Drive [mounted to your computer](https://www.google.com/drive/download/) to get access to the AWS key)

There are two files in the `reports` directory:

```bash
[ec2-user@ip-172-31-29-123 ~]$ ll reports
total 4
-rw-rw-r-- 1 ec2-user ec2-user   0 Jul 31 23:31 copy_database.log
-rwxrwxr-x 1 ec2-user ec2-user 188 Jul 31 23:31 copy_database
```

## How does it work?

Clever little `copy_database` is a simple shell script that copies our production database over to the `josephine-reports` database. When it's done, it updates `copy_database.log` with a timestamp of each successful copy.

We run this script through `chron` periodically to ensure a fresh and cleanclean database. Yay!

Feel free to futz with the schedule by running:

```bash
[ec2-user@ip-172-31-29-123 ~]$ crontab -e
```

Refer to [this guide](http://www.thegeekstuff.com/2009/06/15-practical-crontab-examples/) if you don't remember `cron`'s annoying syntax. Time is in UTC (7 hours ahead).

## Disclaimer
This database uses real user data! So please be careful with it, ya jerk.
