# React-Native

* Installation
* Core concepts
* Best practices
* Best packages

#### This is the Wiki page of Appendgo Kft.'s React-Native development department. <img height="80" style="float:left" src="https://user-images.githubusercontent.com/645053/236628029-2b639e90-a9a2-40f1-ba2d-8d77181ae27a.png">

Mobile Application development: **hello@appendgo.com**

# Guidelines

## Reinvent the wheel

In most platform there is a general truth that says don't reinvent the wheel. If there is an existing package, solution for something which is widely and successfully used, already tested by bunch of people then use that solution in your package.

Now in React-Native it's not entirely true in our experience. There are huge number of packages which are not tested properly, several years old and not maintained, and when you combine a couple of packages together in one screen than comes the real problem.

The guideline here is that you have to review the package carefully! Only use the package if you did a smoke test on it and you're absolutely sure it's okay!

**In your core package you'd better write the components yourself!**

If you find a solution which seems good, check these out:
* Number of bugs (issues)
* When was the last modification
* When was the last release
* * How many users use it
* How many stars does it have

## Common components

Before you start to deal with a component always check the Design how many places is it?
-> If it's more then 1 it should be on a higher level in the project tree, or it should be a common component!

# Installation



