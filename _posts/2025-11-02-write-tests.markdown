---
layout: post
title:  "Just write tests"
date:   2025-11-02 16:12:16 +0000
categories: thoughts 
---

#### Just put ~~fries in a bag, bro~~ tests in tests folder, you're going to need it.

Let's me make things clear, I came from rails background, so what we call unit tests here is actually something that people often refer to as integration tests, meaning it does has a connection to the database and it does calls other classes.
Another thing in which I do believe, that the way how to test is already better, than fully described in https://martinfowler.com/articles/practical-test-pyramid.html.
Now that we've got that out of the way, let's talk about why to test.

I've been working in companies with different philosophies about testing, and sometghing I would like to outline is that e2e test is cool, no doubt, but they are also heavy and brittle.
It takes a lot of resources to run them, and it takes a lot of time to write/fix and understand them. It's because they test the whole scenario, it's not a viable strategy to run them all the time while development. Like you still need them, but not to be run often.

#### 1. Proving code actually works

Once you're done with your code, how do you prove that it works? You can test it manually, but what if you decide to slightly change it? Maybe rename constant used in multiple places, maybe re-arrange functions.
Unit tests give you the possibility to just re-run them and ensure that your code is still working, it is still reachable, and still produces proper results.
Also, you can refer to them as proof of implementation in future.
In a couple of month when documentation for project is gone and jira tickets are purged or lost, you still have a test, which proves that the button is supposed to call pizza and not pasta.

#### 2. Reading code

Let me be honest with you, as a developer, I hate writing documentation, I hate doing diagrams and writing post-mortems, writing code, whatever, for features or bugs are much more fun than retroactively writing documentation. Further more, if we would write documentation for every small feature we implement, we would have no time for shipping actual software, just constant `.md` files, which nobody reads.
However, do I have a solution for you to this? You can always just read a unit test for the given feature. It will give you an understanding of why it works and how it works, while leaving the scope small enough that people don't need to understand whole project.
No, I am serious, you want to understand what code this function does? Read unit test.

Unit tests will also help you onboard new people, as they can just read tests and understand what is happening instead of going around fishing for knowledge.

#### 3. Refactoring

Do you remember the last time you needed to refactor a function or class without changing behaviour? That's where tests would 100% help you.

Want to refactor something? Sure, unit test gets you covered, just keep re-running it while you rewrite code. What do you say? While you are refactoring test keep breaking because you change code? That means you were testing wrong, you need to test behavior, your test doesn't need to know the name of variables, structs, or anything, if your function were writing to the database, it's still writing to the database, that's not changing.

Don't know how something works, but still need to change it? Add unit tests, they will cover you.

#### 4. Covering errors

I think this one has already become a rule, but I prefer to say it outloud, just so there's no confusion for it. I think every bug that you can cover with tests should be covered with tests. It will ensure that you:

1) actually understand the problem
2) actually fixed it
3) have a safeguard against regressions

