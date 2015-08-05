Pivotal Tracker Workflow
==================

Our workflow is very similar to the one they use at Pivotal Labs. It lets you break features up into discrete user stories with clear acceptance criteria. 

You can start by watching [the introductory videos](https://www.pivotaltracker.com/help/gettingstarted) on the official Pivotal Tracker site. They're actually pretty good.

The workflow is pretty simple:

1. Write the story
1. Prioritize the story
1. Estimate the story
1. Start the story
1. Finish the story
1. Deliver the story
1. Accept or Reject the story

Lather, rinse, repeat. This document will explain each step.

## Writing (Good) Stories

Writing a good user story is super important! A good story does far more than just state what's being worked on. A good story helps explain the company's goal, the user's intent, and the exact criteria required for making sure that story is ready to ship.

Here's an example of a poorly written photos.

> **Email unsubscribe**
> Click link in email to unsubscribe

Where do I go to QA this? Who's doing what? Am I logged in? Logged out? How do I know when the feature's ready to ship?

This story could probably be rewritten as:

> **User can unsubscribe from newsletters**
> Given I am a user,
> And I have received any email from Josephine,
> When I click "Unsubscribe,"
> Then I should be sent to a page on Josephine that tells me I am unsubscribed.
> 
> When I check my user settings,
> Then I should no longer be subscribed to the email newsletter.
>
> Given I have already unsubscribed from email newsletters,
> And I have received any email from Josephine,
> When I click "Unsubscribe,"
> Then I should still be unsubscribed.

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
```

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