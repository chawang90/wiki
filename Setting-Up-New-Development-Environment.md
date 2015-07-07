(Assuming OS X Yosemite)

1. Install XCode with command line tools.
1. Install homebrew
1. Run `brew doctor` and fix all issues
1. Run `brew install git`
1. Run `brew install postgresql`
1. Install rvm
1. Clone the repo.
1. Install Ruby version 2.1.0: `rvm install 2.1.0p0`

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
