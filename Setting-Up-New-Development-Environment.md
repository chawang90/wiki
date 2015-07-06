(Assuming OS X Mavericks)

1. install xcode
1. install iterm
1. install homebrew
1. run brew doctor and fix all issues
1. brew install git
1. brew install postgresql
1. install rvm
1. clone the repo
1. install the ruby version it asks for

Add the rvm bootstrapper to your `~/.profile`, `.zshrc`, or whatever:

```
source ~/.rvm/scripts/rvm
```

Install QT for integration tests (capybara depends on nokogiri):

```
brew install qt
```

Install bundler:

```
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
brew install awscli
aws configure
```

Copy production database:

```
sh lib/scripts/copy_production_to_development.sh
```

Run the rails server!

```
rails s
```

Open [localhost:3000](http://localhost:3000). Voila!
