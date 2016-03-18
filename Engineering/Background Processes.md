# Background Processes

We use [DelayedJob](https://github.com/collectiveidea/delayed_job). It's nice for somet things, but we've been thinking of moving off of it since it uses the same database as our application database for serializing and pulling jobs.

## Read This!

By default, **we do not recommend running DelayedJob** unless you're particularly testing for something that will use a background process. Running it will trigger test emails, Slack notifications, etc, and you'll regret all the notifications you get :)

## Clearing Your Jobs

Whenever you've downloaded the database with `jodb`, you've probably inherited some jobs in your queue without even knowing it. You also create queued up jobs while developing locally.

Try the following in a `rails console`:

```ruby
>> Delayed::Job.count
   (0.5ms)  SELECT COUNT(*) FROM "delayed_jobs"
15
```

For that reason, you should always **clear your jobs queue** before running the DelayedJob process.

```
rake jobs:clear
```

Now if you check your Delayed::Job table:

```ruby
>> Delayed::Job.count
   (0.5ms)  SELECT COUNT(*) FROM "delayed_jobs"
0
```

Great! Now you can run DelayedJob.

## Running DelayedJob

Simple as:

```
$ rake jobs:work
[Worker(host:Tals-MacBook-Air.local pid:86239)] Starting job worker
[Worker(host:Tals-MacBook-Air.local pid:86239)] Job UserMailer.signup_confirmation (id=1205238) RUNNING
[Worker(host:Tals-MacBook-Air.local pid:86239)] Job UserMailer.signup_confirmation (id=1205238) COMPLETED after 1.6626
[Worker(host:Tals-MacBook-Air.local pid:86239)] 1 jobs processed at 0.5900 j/s, 0 failed
```

Tada! :tada:
