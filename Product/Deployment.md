Deployment
==========

This is how we deploy code.

1. Code review and :shipit:
---------------------------

Finish writing your code? Someone else will QA it and code review it.

If the code review passes, either the reviewer or reviewee can deploy the thingy.


2. Merge the pull request
------------------------

Code review and QA are good? Awesome.

Make sure the pull request has no conflicts ("This branch is up-to-date with the base branch") and the CI is passing ("All checks have passed")

![](https://dl.dropboxusercontent.com/spa/gcrmzi51hzw4tnm/l8ef5hn4.png)

If it is, go ahead and hit "merge". If you want to be a good citizen (and hopefully you do), you should also delete the remote branch, since it's no longer needed.

> placeholder image for "delete branch"

Great! Now the code is on Github's master branch. Let's pull that down and deploy it to Heroku.

3. Deploy the code!
--------------------

Go to your terminal and check out the master branch.

```bash
$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
```

Pull down the latest master:

```bash
$ git pull --rebase
remote: Counting objects: 1, done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), done.
joFrom github.com:josephine/josephine
   6a22e7b..a0e59d4  master     -> origin/master
dFirst, rewinding head to replay your work on top of it...
eFast-forwarded master to a0e59d450bbbf4a10ce9c29f4779089e7ed6b733.
```

Make sure that there are no errors or merge conflicts! If there are, something funky might be happening.

If everything's good, run the deploy command:

```bash
$ jodeploy production
Pushing to Github..
Everything up-to-date
Pushing to production...
Counting objects: 36, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (36/36), done.
Writing objects: 100% (36/36), 3.61 KiB | 0 bytes/s, done.
Total 36 (delta 27), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote:
remote: -----> Using set buildpack heroku/ruby
remote: -----> Ruby app detected
remote: -----> Compiling Ruby/Rails
remote: -----> Using Ruby version: ruby-2.2.3
remote: -----> Installing dependencies using bundler 1.9.7
remote:        Running: bundle install --without development:test --path vendor/bundle --binstubs vendor/bundle/bin -j4 --deployment
remote:        Using rake 10.4.2
remote:        Using i18n 0.7.0
remote:        Using json 1.8.3
remote:        Using minitest 5.8.0
remote:        Using thread_safe 0.3.5
remote:        Using builder 3.2.2
remote:        Using erubis 2.7.0
remote:        Using mini_portile 0.6.2
remote:        Using rack 1.6.4
remote:        Using mime-types 2.6.1
remote:        Using arel 6.0.3
remote:        Using addressable 2.3.8
remote:        Using multi_json 1.11.2
remote:        Using analytics-ruby 2.0.12
remote:        Using bcrypt 3.1.10
remote:        Using multi_xml 0.5.5
remote:        Using multipart-post 2.0.0
remote:        Using jwt 1.5.1
remote:        Using browser 1.0.1
remote:        Using daemons 1.2.3
remote:        Using mimemagic 0.3.0
remote:        Using unf_ext 0.0.7.1
remote:        Using eventmachine 1.0.8
remote:        Using excon 0.45.4
remote:        Using execjs 2.6.0
remote:        Using thor 0.19.1
remote:        Using hike 1.2.3
remote:        Using jcrop-rails-v2 0.9.12.3
remote:        Using sass 3.2.19
remote:        Using kgio 2.10.0
remote:        Using mixpanel-ruby 2.2.0
remote:        Using netrc 0.10.3
remote:        Using newrelic_rpm 3.13.0.299
remote:        Using bundler 1.9.7
remote:        Using tilt 1.4.1
remote:        Using pg 0.18.3
remote:        Using possessive 1.0.1
remote:        Using rails_serve_static_assets 0.0.4
remote:        Using rails_stdout_logging 0.0.4
remote:        Using raindrops 0.15.0
remote:        Using slack-notifier 1.3.0
remote:        Using temple 0.7.6
remote:        Using standard_deviation 1.0.3
remote:        Using will_paginate 3.0.7
remote:        Using tzinfo 1.2.2
remote:        Using nokogiri 1.6.6.2
remote:        Using mail 2.6.3
remote:        Using css_parser 1.3.6
remote:        Using rack-test 0.6.3
remote:        Using httparty 0.13.5
remote:        Using faraday 0.9.1
remote:        Using unf 0.1.4
remote:        Using thin 1.6.3
remote:        Using mandrill-api 1.0.53
remote:        Using uglifier 2.7.2
remote:        Using foreman 0.78.0
remote:        Using airbrake 4.3.1
remote:        Using twilio-ruby 3.16.1
remote:        Using rails_12factor 0.0.3
remote:        Using unicorn 4.9.0
remote:        Using will_paginate-bootstrap 1.0.1
remote:        Using activesupport 4.2.3
remote:        Using loofah 2.0.3
remote:        Using aws-sdk-v1 1.66.0
remote:        Using roadie 3.0.5
remote:        Using oauth2 1.0.0
remote:        Using domain_name 0.5.24
remote:        Using sprockets 2.12.4
remote:        Using slim 3.0.6
remote:        Using rails-deprecated_sanitizer 1.0.3
remote:        Using globalid 0.3.6
remote:        Using activemodel 4.2.3
remote:        Using climate_control 0.0.3
remote:        Using delayed_job 4.0.6
remote:        Using rails-html-sanitizer 1.0.2
remote:        Using bitly 0.10.4
remote:        Using http-cookie 1.0.2
remote:        Using rails-dom-testing 1.0.7
remote:        Using activejob 4.2.3
remote:        Using activerecord 4.2.3
remote:        Using cocaine 0.5.7
remote:        Using delayed-plugins-airbrake 1.1.0
remote:        Using rest-client 1.8.0
remote:        Using actionview 4.2.3
remote:        Using delayed_job_active_record 4.0.3
remote:        Using friendly_id 5.1.0
remote:        Using nilify_blanks 1.2.1
remote:        Using paperclip 4.3.0
remote:        Using aws-sdk 1.66.0
remote:        Using stripe 1.25.0
remote:        Using actionpack 4.2.3
remote:        Using delayed_paperclip 2.9.1
remote:        Using actionmailer 4.2.3
remote:        Using railties 4.2.3
remote:        Using sprockets-rails 2.3.3
remote:        Using simple_form 3.1.1
remote:        Using jquery-fileupload-rails 0.4.5
remote:        Using jquery-rails 4.0.5
remote:        Using rails 4.2.3
remote:        Using roadie-rails 1.0.6
remote:        Using sass-rails 4.0.5
remote:        Using papercrop 0.2.0
remote:        Using rails_autolink 1.1.6
remote:        Using sql_queries_count 0.0.1
remote:        Bundle complete! 62 Gemfile dependencies, 104 gems now installed.
remote:        Gems in the groups development and test were not installed.
remote:        Bundled gems are installed into ./vendor/bundle.
remote:        Bundle completed (0.45s)
remote:        Cleaning up the bundler cache.
remote: -----> Preparing app for Rails asset pipeline
remote:        Running: rake assets:precompile
remote:        Asset precompilation completed (2.30s)
remote:        Cleaning assets
remote:        Running: rake assets:clean
remote:
remote:
remote: -----> Discovering process types
remote:        Procfile declares types     -> postgres, web
remote:        Default types for Multipack -> console, rake, worker
remote:
remote: -----> Compressing... done, 63.4MB
remote: -----> Launching... done, v1107
remote:        https://josephine-members.herokuapp.com/ deployed to Heroku
remote:
remote: Verifying deploy... done.
To git@heroku.com:josephine-members.git
   b003cb8..a0e59d4  master -> master
Running migration...
```

The `jodeploy` command does a lot:
- pushes master to Github
- pushes master up to Heroku
- runs migrations

You can see how it works in [`.shell-commands`](https://github.com/josephine/www/blob/master/.shell-commands)

4. Celebrate :tada:
-------

That's it! Congratulations on your deploy.

You should see an otification
