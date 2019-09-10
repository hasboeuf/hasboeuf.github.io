---
layout: post
title: yogit presentation
date: 2019-10-10 00:21:06 +0100
author: Adrien Gavignet
categories: yogit github
---

**TL;DR:** [How to install & documentation](https://pypi.org/project/yogit/)

I recently published `yogit`, a CLI tool that helps developers during daily work.

Well, only if you are using GitHub and particularly if you:

* work on multiple repositories
* use pull requests and GitHub reviews
* like to cleanup branches
* share your daily contributions to your team
* like stats

Let's see how `yogit` can help (non-exhaustive).

## Pull requests

I'm working in a company that have hundreds of repositories (no shit), `git` submodules are heavily used, stories and tasks are sometimes paused. Through time, some pull requests require upmerge or conflict resolving, it's not easy to keep an eye on everything.

`yogit pr list` will list your opened pull requests and tell if they're still mergeable or rather conflicted.

## Reviews

Code reviews are part of our job, here again `yogit` will help you to track reviews you've made.

`yogit review requested` will list pull requests on which your review is required.

`yogit review list` will list reviews you've made on pull requests (still opened) and will warn you if new commits have been pushed since your last check. Trust but verify as we say :)

## Branches

Ok, what "proofs of concept", "fix attempts", "abandonned features" etc, have in common? They all have one branch. Sometimes a cleanup is advised to avoid confusions.

`yogit branch list [--dangling]`: will list all your branches with their associated pull requests, if none, think about it and clean :)

## Contributions

From GitHub point of view, a contribution is either a pull request opened or a review made.

`yogit contrib list` will list your contributions for a given date range.

If you're a number man, `yogit contrib stats` might interest you ;)

## Organization

Several commands related to organization are available, I let you discover them, teaser: `yogit orga member pickone`.

## SCRUM

If you are used to write a daily report to your team, `yogit scrum report` can help you achieve it. By default it will ask you few questions (today/blockers/tomorrow questions) and append your contributions of the day. But questions and report format are customizable.

## That's it

Documentation is here [https://pypi.org/project/yogit/](https://pypi.org/project/yogit/) and ... bugs can be reported here [https://github.com/hasboeuf/yogit](https://github.com/hasboeuf/yogit) ;)

Hope `yogit` will save you some time :)
