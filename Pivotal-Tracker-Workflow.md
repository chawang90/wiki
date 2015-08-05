Pivotal Tracker Workflow
==================

Our workflow is very similar to the one they use at Pivotal Labs. It lets you break features up into discrete user stories with clear acceptance criteria. 

You can start by watching [the following videos](https://www.pivotaltracker.com/help/gettingstarted) on the official Pivotal Tracker site:
- Getting Started
- Writing Stories
- Prioritizing and Estimating Complexity
- Delivering Stories

## Writing Good Stories

Writing a good user story.

Further Reading:

- [Be Good To Your Devs: Write User Stories That Are Easy To Understand](http://pivotallabs.com/write-user-stories-that-are-easy-to-understand/)
- [How to write Well-Formed User Stories](http://pivotallabs.com/well-formed-stories/)

- Use Gherkin. Define clear setup and acceptance criteria.
- Features
- Bugs
- Chores
- Release Flags

## Starting Stories

Hit "Start" when you begin working on a story. This lets everyone else on the team know you're handling it. If there are other stories that are related and you want to take them on, hit Start on them too.

Stories that are started will have the **Finish** button next to them.

## Finishing Stories

Hit **Finish** when you finish writing all of the code for this story.

In most cases, it makes sense for the commit title to be the same title as the story. In the notes, feel free to include additional information (make use of bullets, @mentions, etc). Finally, it's a nice touch to Finish the story directly from your commit message.

Here's an example.
```
Some example.
``

In general, we prefer having one commit per feature as opposed to a series of many. If a story requires too much code, there's a good chance it could be broken up into smaller stories with more discrete 

If you prefer working with small commits, you can always "squash" your commits into one commit at the end using `git rebase --interactive`. If you're unfamiliar with interactive rebasing, talk to Tal and he'll show you. It's pretty rad but can be dangerous if you mess it up.

Stories that are Finished will have the **Deliver** button next to them.

## Delivering Stories

Once you've finished writing your code, you should put the features on staging for acceptance.

First, review the initial story and make sure the acceptance criteria are clear: who's the user, what are they doing, and what are they expecting to happen? Are there edge case scenarios we didn't think of initially? If you've elaborated on the original story, make sure to 

Stories that are Delivered will have the **Accept** and **Reject** buttons next to them.

## Accepting or Rejecting Stories

The code is on staging. What now?

Open up the story and . If something isn't clear about the acceptance criteria, talk to the developer who wrote the code and update the story