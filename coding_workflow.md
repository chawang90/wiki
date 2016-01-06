tl;dr
------------
1. **Create an issue** in Zenhub. It'll give you an issue number, like 145.
1. **Drag your issue** into "In Progress" when you start working.
2. **Create a local branch** from master with `git checkout -b <branch_name>`. Do your work.
3. Push your branch up to a **remote branch** with `git push -u origin HEAD` when you're ready to share.
4. **Open a pull request** using `hub pull-request -i <issuenumber>`
5. **Get feedback** and keep working.
6. Drag into **Ready For Review** when you're done!
7. When another person approves your change, **merge your branch** by clicking "Merge Pull Request" (a rebase may be necessary)
8. **Deploy Your Code**: First check out master and pull it down. Then run `jodeploy production`. This pushes to Github, pushes to Heroku, runs `rake db:migrate`, and sends a Slack notification.
9. **You're done!** Pat yourself on the back. Or pat someone else :)

## Creating an Issue in Zenhub

> We use [Zenhub](https://www.zenhub.io/), which is an relatively new product management tool that integrates directly with Github Issues. When you install the chrome extension and your Github Issues will look like this:

New issues get filed into **New Issues**. They can get filed by anyone on the team, but once they're filed someone on the product team to make sure that the story has all the information necessary (spec, context, goal, etc).

![](https://dl.dropboxusercontent.com/spa/gcrmzi51hzw4tnm/r3keprw-.png)

## Github Flow + Review Apps

We use the Github's "Github Flow" method.

> https://guides.github.com/introduction/flow/

Basically, you start a branch when you work on something new. When you're ready to share it, you create a pull request. When the pull request is ready to be reviewed, share it with the other developers and/or product people on the team.

Everyone on the team can easily access a live, working version of your pull request via Heroku Review Apps. For example, pull request #134 (https://github.com/josephine/josephine/pull/134) will be accessible on a staging environment automagically! (https://josephine-staging-pr-134.herokuapp.com/)

![](https://dl.dropboxusercontent.com/spa/gcrmzi51hzw4tnm/049swski.png)


## Style Guides

Coding style is serious business! Let's be consistent and beautiful.

- Ruby: https://github.com/bbatsov/ruby-style-guide
- Javascript: https://github.com/airbnb/javascript/tree/master/es5
- CSS: https://medium.com/@fat/mediums-css-is-actually-pretty-fucking-good-b8e2a6c78b06
- Git: https://github.com/agis-/git-style-guide
