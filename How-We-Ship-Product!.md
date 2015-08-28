# How We Ship Product!

Tell me how!

Our workflow is very similar to the one they used at Pivotal Labs. We break groups of features ("epics") up into discrete user stories with clear acceptance criteria. This document will explain the jargon, methodology, and rationale behind why we do this.

[The introductory videos](https://www.pivotaltracker.com/help/gettingstarted) on the official Pivotal Tracker site are actually pretty good. Have a look! It's a good primary source.

So what's the workflow?

#### Prioritizing Epics

An "epic" is a big chunks of features. We talk about epics at the Friday product prioritization meeting, and they generally represent work for the next 2-3 months of work (though sometimes longer term).

We use Trello to keep track of epics. Each card represents one epic, and may have additional notes, preliminary speccing and estimation, but for the most part these are super rough.

An example of an epic would be "A La Carte Ordering" or "Meal Labels." We drag these around and use them to decide what to work on next, based on business priorities and estimation / scoping. 

For the most part epics are actually composed of many different things we need built. These things are "stories."


#### Stories

A "story" is:

> Anything a user can do or see on the website that they previously couldn't. When we write the story, we describe what a user's intention is, the steps they should take, and the results that they expect.

*(If we're getting nitpicky, we could also have stories that remove funtionality. But who's counting.)*

If we take the "Dietary Labels" epic for example, and break it up into stories, we might get:

- "Customer can see dietary information on the meal page"
- "Customer can see dietary information on the search results page"
- "Customer can set dietary preferences" 
- "Cook can set dietary information for their meal"

Each of these has their own "acceptance criteria," meaning –– how do I QA this feature and ensure that it's done? But We'll get to that.

#### The Pivotal Acceptance Process

"Acceptance" is what we want. When a story is "accepted," it means that it meets all the different requirements for us to ship it to the live site.

"Acceptance" is the final stage of a story's lifecycle. How do we get there?

1. Write the story
1. Prioritize the story
1. Estimate the story
1. Start the story
1. Finish the story
1. Deliver the story
1. Accept the story (or Reject it)

Lather, rinse, repeat. This document will explain each step, and then end with some pro tips on how to communicate more effectively with Pivotal.

## Writing (Good) Stories

Writing a good user story is super important! A good story does far more than just state what's being worked on. A good story helps explain the company's goal, the user's intent, and the exact criteria required for making sure that story is ready to ship.

### An example

Let's take a look at this story:

```
Title: Addon Items
Description: 
```

![](https://dl.dropboxusercontent.com/spa/gcrmzi51hzw4tnm/ohs5k393.png)

How do I QA this? Who does what? Am I logged in? Logged out? How do I know when the feature's ready to ship?

This story could probably be rewritten as:

### Types of Stories
- Features
- Bugs
- Chores
- Release Flags


### Further Reading:

- [Be Good To Your Devs: Write User Stories That Are Easy To Understand](http://pivotallabs.com/write-user-stories-that-are-easy-to-understand/)
- [How to write Well-Formed User Stories](http://pivotallabs.com/well-formed-stories/)


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

## Accepting Stories

The code is on staging. What now?

Open up the story and . If something isn't clear about the acceptance criteria, talk to the developer who wrote the code and update the story

## Rejecting Stories

If anything wrong with the feature –– a big gaping bug, a copy or design tweak, an edge case or even just something that feels wrong, reject the story!

When rejecting a story, leave as much information as possible: here's what I did, here's what I expected, and here's what happened. The more specific you are, the better!

Meh:
> it created two stories

Better:
> I just published a meal and it looks like it created two "Published Meal" events instead of one. Here's a screenshot of the first [screenshot] and here's a screenshot of the second [screenshot].

## Better Communication