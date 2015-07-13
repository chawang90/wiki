# Setting Up the Development Environment

This setup guide assumes you're using OS X Mavericks.

Install xcode. When it's done you might need to also install the command line tools with this command:

```
xcode-select --install
```

Install homebrew. There's a one-liner at [http://brew.sh/](http://brew.sh/).
Then brew install some stuff needed by rvm and capybara/nokogiri:

```
brew install gpg qt postgresql awscli
```

Clone the repo

```
git clone git@github.com:josephine/josephine.git
```

## Rubies

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

Download and install the [Heroku Toolbelt](https://toolbelt.heroku.com/)

Add production & staging Heroku git remotes:

```
git remote add production git@heroku.com:josephine-members.git
git remote add staging git@heroku.com:josephine-staging.git
```

Set up AWS for S3 assets. (Get access keys from Tal)

```
aws configure
```

Enter access key and secret access key. Leave the `region name` and `output format` blank.

Copy production database:

```
sh lib/scripts/copy_production_to_development.sh
```

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
