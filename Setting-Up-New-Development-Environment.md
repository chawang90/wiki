(Assuming OS X Mavericks)

install xcode

(install iterm)

install homebrew
run brew doctor and fix all issues
brew install git
brew install postgresql

install rvm

clone the repo

install the ruby version it asks for

run bundle

install heroku toolbelt

add production & staging remotes
git remote add production git@heroku.com:josephine-members.git
git remote add staging git@heroku.com:josephine-staging.git

copy production database
sh lib/scripts/copy_production_to_development.sh

run rails s -- should work!

voila!