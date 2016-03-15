# Setting Up  Your Development Environment

Oh, development environment setup. Fun!

It's best to run through this doc in order, since certain things are dependent on each other! If something seems outdated, a step is missing, or something flat out feels wrong, make it better!

Okay, let's jump in!

## Install Xcode

We begin by installing Xcode, so [do that here](https://developer.apple.com/xcode/download/). Use the App Store link. It may take a while.

Once Xcode is set up, you'll also want to install the command line tools.

```
xcode-select --install
```

It's important to do this first, since it'll affect other things you install later on.


## Install Homebrew

Next, we'll install Homebrew.

Run the one-liner found at [http://brew.sh/](http://brew.sh/). Make sure to read the post-install instructions all the way through so you know you're good!

When you're done, run `brew doctor`:

```
brew doctor
```

... and fix everything it asks you to fix.

### Install Homebrew Packages

Now that Homebrew's installed, let's `brew install` some stuff.

Run the following one at a time (and follow the post-install instructions all the way through!):

```bash
brew install gpg
brew install qt
brew install libiconv
brew install postgresql
brew install phantomjs

brew install openssl
brew unlink openssl
brew link openssl --force

brew install graphviz
brew install awscli
brew install node
brew install imagemagick

brew install hub
brew install heroku-toolbelt
```

## Get our code!

Your Github account should have been added to our organization. If it hasn't, ask a developer and they'll add you!

#### SSH Keys

Since this is a new computer, chances are you don't have SSH keys set up. Follow Github's guides here:

- [Generating an SSH key and adding it to ssh-agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
- [Adding an SSH key to your Github ccount](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)

#### Clone the repo

Once your SSH keys are set up, you should be able to clone the repo:

```
git clone git@github.com:josephine/www.git
```

## Install RVM and Ruby

We use RVM for managing Ruby versions and gemsets.

#### Install RVM

There's a nice two-liner at [https://rvm.io/](https://rvm.io/). Run it! (and yes, follow all the instructions :)

#### Install Ruby

Now you can `cd` into the `www` directory (`cd` out of it if you're already there)

```
cd www
```

You'll know `rvm` is working because you'll see a warning that says something like:

```
ruby-2.x.x is not installed.
To install do: 'rvm install ruby-2.x.x'
```

Go ahead and run the `rvm install` command it gives you. It installs a fresh version of Ruby (specified in our `.ruby-version` file), so it may take a while.

When it's done, run the following to make sure everything worked:

```
$ ruby --version
ruby 2.2.3p173 (2015-08-18 revision 51636) [x86_64-darwin14]

$ which ruby
/Users/tal/.rvm/rubies/ruby-2.2.3/bin/ruby
```

## Install Gems

Since this is a new machine, you'll need to install bundler:

```
gem install bundler
```

Then install the our gems (make sure you're still in the `www` directory)

```
bundle
```

Great! You can check that this worked by running:

```
$ rails --version
Rails 4.2.4
```

## Add Heroku Remotes

Download and install the [Heroku Toolbelt](https://toolbelt.heroku.com/)

Add Heroku git remotes:

```
git remote add production git@heroku.com:josephine-production.git
git remote add staging git@heroku.com:josephine-staging.git
git remote add reports git@heroku.com:josephine-reports.git
git remote add config git@heroku.com:josephine-config.git
```

#### The `josephine-config` app

We use a dummy Heroku app (`josephine-config`) to store our shared development configuration.

Pull down the development configuration toadd all required environment
variables to `.env`. See https://github.com/ddollar/heroku-config for more info.

```sh
heroku plugins:install https://github.com/ddollar/heroku-config.git
heroku config:pull -r config
```

## Shell commands

We have a set of shell commands we use to make working on Josephine easier. They're currently in the `.shell-commands` file in the `www` repo, but may get moved in to a separate `josephine-cli` project in the future.

Add the following to your `.bash_profile` to get the Josephine shell commands:

```
source ~/PATH-TO-YOUR-JOSEPHINE-PROJECT/.shell-commands`
```

You'll need to refresh your terminal(s) by running:

```
source ~/.bash_profile
```

## Download the database

Good thing you installed the Josephine shell commands in the previous section!

We'll use the `jodb` command to make a local (sanitized) copy of the database. Run the following:

```
jodb development
```

## Download S3 assets

We use AWS for S3 assets. To get the access keys, run:

```
heroku config -r config | grep -i aws

AWS_SECRET_ACCESS_KEY = ...
AWS_ACCESS_KEY_ID = ...
```

Then run `aws configure`:

```
aws configure
```

Enter the `access key` and `secret access key` from above. Make the `region name=us-west-1` and leave the `output format` blank.

Now you can use another Josephine command, `jos3`, to copy over

```
jodb development
```

## Running the App

Database? Check. Assets? Check. We're ready to run the server!

```
rails server
```

Open [localhost:3000](http://localhost:3000). Voila!

## Running the test suite

We also want to make sure our lovely test suite passes on your machine. Run it!

```bash
# Create a test database mirroring the development database's schema
rake db:test:prepare

# Run the tests!
rspec spec/
```

Hopefully it's all green! :green_heart: :green_apple: :recycle: :green_book: :smile:

## Celebrate :tada:

Always important to celebrate.
