# Setting Up  Your Development Environment

This setup guide assumes you're using OS X Mavericks.

## xcode

Install xcode. When it's done you might need to also install the command line tools with this command:

```
xcode-select --install
```

## Homebrew

Install homebrew. There's a one-liner at [http://brew.sh/](http://brew.sh/). Read the post-install instructions carefully! Run `brew doctor` until it stops yelling at you.

Then brew install some stuff needed by rvm and capybara/nokogiri:

```
brew install gpg qt postgresql awscli phantomjs graphviz
```

## Git

Clone the repo:

```
git clone git@github.com:josephine/josephine.git
```

## Ruby and RVM

Install rvm. There's a two-liner at [https://rvm.io/](https://rvm.io/).
Then add the rvm bootstrapper to your `~/.profile`, `.zshrc`, or whatever:

```
source ~/.rvm/scripts/rvm
```

Now you can `cd` into the josephine directory:

```
cd josephine
```

You'll know `rvm` is working because you'll see a warning that says something like

```
ruby-2.2.3 is not installed.
To install do: 'rvm install ruby-2.2.3'
```

Go ahead and run the `rvm install` command.

# Installing Gems

Install bundler, and run the `bundle` command to install all of our gems:

```
gem install bundler
bundle
```

## Issues installing capybara-webkit

Capybara depends on on Nokogiri, which has all sorts of dependencies. You might see your `bundle install` fail on installing Nokogiri, with this message:

```
libiconv is missing.  Please locate mkmf.log to investigate how it is failing.
-----
*** extconf.rb failed ***

[..]

extconf failed, exit code 1

Gem files will remain installed in /Users/cristian/.rvm/gems/ruby-2.1.5@global/gems/nokogiri-1.6.6.2 for inspection.
Results logged to /Users/cristian/.rvm/gems/ruby-2.1.5@global/extensions/x86_64-darwin-14/2.1.0-static/nokogiri-1.6.6.2/gem_make.out
An error occurred while installing nokogiri (1.6.6.2), and Bundler cannot continue.
Make sure that `gem install nokogiri -v '1.6.6.2'` succeeds before bundling.
```

If that's the case, try running this command:

```
brew install libiconv
```

You also might see it fail on installing `capybara-webkit`. In that case, run this command:

```
brew install qt
```

## Heroku

Download and install the [Heroku Toolbelt](https://toolbelt.heroku.com/)

Add Heroku git remotes:

```
git remote add production git@heroku.com:josephine-production.git
git remote add staging git@heroku.com:josephine-staging.git
git remote add reports git@heroku.com:josephine-reports.git
git remote add config git@heroku.com:josephine-config.git

```

We use a dummy Heroku app (`josephine-config`) to store our shared development configuration. Pull down the development configuration to  add all required environment
variables to `.env`. See https://github.com/ddollar/heroku-config for more info.

```sh
heroku plugins:install https://github.com/ddollar/heroku-config.git
heroku config:pull -r config
```

## Shell Helpers for Deployment and Copying Databases

We've written some handy shell functions that are checked into the repository in `.shell-helpers`.

Add this line to your `.bash_profile` (or equivalent) to get access to them:

```
source [PATH_TO_JOSEPHINE_DIRECTORY]/.shell-commands
```

Reload your shell, then:

```
jodeploy staging
jodeploy production
```

## AWS / Assets / Database

Set up AWS for S3 assets. (Get access keys from Tal)

```
aws configure
```

Enter access key and secret access key. Leave the `region name` and `output format` blank.

Copy production database to your development environment:

```
jodb development
```

## Running the App

Run the rails server!

```
rails server
```

Open [localhost:3000](http://localhost:3000). Voila!

## Running Tests

```
rake db:test:prepare
rspec spec/
```

Hopefully it's all :green_heart: :green_apple: :recycle: :green_book: :smile:
