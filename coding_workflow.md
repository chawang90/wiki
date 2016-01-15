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

## Git Merging and Rebasing

So you worked on your branch and you're done. But you see that your code is no longer up to date with master.

![](https://photos-1.dropbox.com/t/2/AABWlkMpxZq_E9ZbL_33DnJdE2rI8Zcrpn6tuJGqJprjsQ/12/17893089/png/32x32/1/_/1/2/Screenshot%202016-01-15%2013.21.13.png/EKG7qg0Y8vwGIAIoAg/B8WXSKlpEFGRCfK9qpxqnXklACbCD-IG-zmDNVxx_Ws?size=1280x960&size_mode=3)

You need to rebase!

First, go to master and make sure it's up to date:

```bash
git checkout master
git pull --rebase
```

Great. Now go back to your branch and rebase master on top of it.

```bash
git checkout my_branch
git rebase master
```

Rebasing will show you your file conflicts.
```bash
joy at Joy-Dings-MacBook-Air in ~/josephine on admin-can-create-neighborhood
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: Admin can navigate to new neighborhood screen.
Applying: Admin can create neighborhood from new neighborhood screen.
Using index info to reconstruct a base tree...
M	config/locales/en.yml
M	config/routes.rb
M	db/schema.rb
<stdin>:38: trailing whitespace.
<%= simple_form_for(Neighborhood.new, url: admin_neighborhoods_path) do |f| %> 
<stdin>:165: trailing whitespace.
feature 'Admin creates new neighborhood' do  
warning: 2 lines add whitespace errors.
Falling back to patching base and 3-way merge...
Removing lib/neighborhood.rb
Auto-merging db/schema.rb
CONFLICT (content): Merge conflict in db/schema.rb
Auto-merging config/routes.rb
Auto-merging config/locales/en.yml
Failed to merge in the changes.
Patch failed at 0002 Admin can create neighborhood from new neighborhood screen.
The copy of the patch that failed is found in:
   /Users/joy/josephine/.git/rebase-apply/patch

When you have resolved this problem, run "git rebase --continue".
If you prefer to skip this patch, run "git rebase --skip" instead.
To check out the original branch and stop rebasing, run "git rebase --abort".
```
Resolve the issue in each file, add them, and continue the rebase. You may have to do this more than once (unfortunately).
```bash 
$ git st
On branch admin-can-create-neighborhood
Your branch and 'origin/admin-can-create-neighborhood' have diverged,
and have 90 and 25 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)
nothing to commit, working directory clean
```


Wee! Finally, **force push** your branch back up to the remote. **BE EXTRA CAREFUL THAT YOU'RE NOT ON MASTER WHEN YOU FORCE PUSH.**

```bash
git push -f origin head
```

## Style Guides

Coding style is serious business! Let's be consistent and beautiful.

- Ruby: https://github.com/bbatsov/ruby-style-guide
- Javascript: https://github.com/airbnb/javascript/tree/master/es5
- CSS: https://medium.com/@fat/mediums-css-is-actually-pretty-fucking-good-b8e2a6c78b06
- Git: https://github.com/agis-/git-style-guide
