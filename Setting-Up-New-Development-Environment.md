# Setting Up the Development Environment

This setup guide assumes you're using OS X Mavericks.

## xcode

Install xcode. When it's done you might need to also install the command line tools with this command:

```
xcode-select --install
```

## Homebrew

Install homebrew. There's a one-liner at [http://brew.sh/](http://brew.sh/).
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
git remote add dev git@heroku.com:josephine-dev.git
```

Pull down the development configuration. This will add all required environment
variables to `.env`. See https://github.com/ddollar/heroku-config#usage for more info.

```sh
heroku plugins:install git://github.com/ddollar/heroku-config.git
heroku config:pull -r dev
```

## AWS / Assets / Database

Set up AWS for S3 assets. (Get access keys from Tal)

```
aws configure
```

Enter access key and secret access key. Leave the `region name` and `output format` blank.

Copy production database:

```
sh lib/scripts/copy_production_to_development.sh
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
