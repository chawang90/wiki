## Setup

1. Make sure you have a Github account. If you don't, sign up for Github, and ping the product team with your username, so we can add you.
1. Add Zenhub (currently only works in Chrome) https://www.zenhub.io/.
It should show up in the extensions section of your Chrome browser as a Z with a blue background. Click on the Z and sign in with your Github account details.
![test](https://www.dropbox.com/s/5zlc6o45834e2wd/Screenshot%202015-09-25%2015.40.57.png?dl=0)
1. Once you have Zenhub, sign in to Github and then go to https://github.com/josephine/josephine#boards?repos=18314977

## How to file a good bug :bug: :beetle:

Once you've discovered whether it's a bug,
is it a bug?

ask the user questions
- are you logged in?
- has this happened before?
- what device are you using?
- what browser are you using?
- what operating system are you using?


take down notes
- user id (or name so you can find it later)
- meal
- what are they trying to order

writing the bug.

**read this guide first**. https://sifterapp.com/blog/2012/08/tips-for-effectively-reporting-bugs-and-issues/

okay so it's a bug! the most important thing is helping to document how someone else can re-create this bug.

```
Given I am ________.
When I __________.
Then I should ____________.
```

```
Given I am a logged in user,
And I am on a meal page,
When I click
```

more information is always better than less
"it doesn't work"

> If you have to report a bug to a programmer who can't be present in person, the aim of the exercise is to enable them to reproduce the problem. You want the programmer to run their own copy of the program, do the same things to it, and make it fail in the same way. When they can see the problem happening in front of their eyes, then they can deal with it.

read these!

- https://sifterapp.com/blog/2012/08/tips-for-effectively-reporting-bugs-and-issues/
- http://sqa.stackexchange.com/questions/1920/best-guidelines-for-bug-reporting
