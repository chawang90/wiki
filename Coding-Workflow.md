tl;dr
------------
1. Create an issue in Zenhub. It'll give you an issue number, like 145.
1. Drag your issue into "In Progress" when you start working.
2. Create a local branch. Do your work.
3. Push up to remote branch when you're ready to share.
4. Open a pull request using `hub pull-request -i <issuenumber>` 
5. Get feedback and keep working.
6. Drag into "Ready For Review" when you're done!
7. When another person approves your change, you can merge using `Merge Pull request`. A rebase may be necessary. 
8. Pull down local changes by refreshing master. Deploy your code from master and run `jodeploy production`. This pushes to github, pushes to heroku, runs rake dbmigrate, and sends a slack notification.
9. You're done! Pat yourself on the back. Or pat someone else :)

Story Tracking
--------------

We use [Zenhub](https://www.zenhub.io/), which is an relatively new product management tool that integrates directly with Github Issues.

When you install the chrome extension and your Github Issues will look like this:

![](https://dl.dropboxusercontent.com/spa/gcrmzi51hzw4tnm/r3keprw-.png)

New issues get filed into **New Issues**. They can get filed by anyone on the team, but once they're filed someone on the product team to make sure that the story has all the information necessary (spec, context, goal, etc).



Github Flow + Review Apps
-------

We use the Github's "Github Flow" method.

> https://guides.github.com/introduction/flow/

Basically, you start a branch when you work on something new. When you're ready to share it, you create a pull request. When the pull request is ready to be reviewed, share it with the other developers and/or product people on the team.

Everyone on the team can easily access a live, working version of your pull request via Heroku Review Apps. For example, pull request #134 (https://github.com/josephine/josephine/pull/134) will be accessible on a staging environment automagically! (https://josephine-staging-pr-134.herokuapp.com/)

![](https://dl.dropboxusercontent.com/spa/gcrmzi51hzw4tnm/049swski.png)


Style Guides
------------

Coding style is serious business! Let's be consistent and beautiful.

- Ruby: https://github.com/bbatsov/ruby-style-guide
- Javascript: https://github.com/airbnb/javascript/tree/master/es5
- CSS: https://medium.com/@fat/mediums-css-is-actually-pretty-fucking-good-b8e2a6c78b06
- Git: https://github.com/agis-/git-style-guide
