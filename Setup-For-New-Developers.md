# Setting Up  Your Development Environment

This setup guide assumes you're using OS X Mavericks.

## xcode

Install xcode. When it's done you might need to also install the command line tools with this command:

```
xcode-select --install
```

## libiconv

Capybara depends on on Nokogiri, which has this bad boy as a dependency. You might see your `bundle install` fail on installing Nokogiri, with this message:

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

## Ruby

Install rvm. There's a two-liner at [https://rvm.io/](https://rvm.io/).
Then add the rvm bootstrapper to your `~/.profile`, `.zshrc`, or whatever:

```
source ~/.rvm/scripts/rvm
```

When you `cd` into the josephine app directory, you'll know `rvm` is working because you'll see a warning that says something like

```
ruby-2.2.3 is not installed.
To install do: 'rvm install ruby-2.2.3'
```
Go ahead and run the `rvm install` command.

Install bundler:

```
cd josephine
gem install bundler
bundle
```

## Heroku

Download and install the [Heroku Toolbelt](https://toolbelt.heroku.com/)

Add Heroku git remotes:

```
git remote add production git@heroku.com:josephine-members.git
git remote add staging git@heroku.com:josephine-staging.git
git remote add reports git@heroku.com:josephine-reports.git
git remote add dev git@heroku.com:josephine-dev.git

```

Pull down the development configuration. This will add all required environment
variables to `.env`. See https://github.com/ddollar/heroku-config#usage for more info.

```sh
heroku plugins:install git://github.com/ddollar/heroku-config.git
heroku config:pull -r dev
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
rake db:create db:migrate
rake db:test:prepare
rspec spec/features
```