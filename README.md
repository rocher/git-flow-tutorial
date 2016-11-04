<!--*- mardown-mode, auto-fill, flyspell -*-->

# [ *work in progress* ]

---

# GitHub + git-flow Tutorial

## Introduction
This tutorial shows how to use GitHub
and [git-flow](https://github.com/petervanderdoes/gitflow-avh) together.

To show in detail the use of git-flow, this tutorial is developed around an
imaginary open-source project called `foobar` (yes, seriously), developed by a
team of software developers. In this scenario, following actors are supposed to
exist:

  1. a *maintainer*, responsible to announce, publish and release new versions,
     make hot fixes and give support to old releases
  2. an *integrator*, responsible of the continuous integration of the features
     the team is producing and to provide a suitable environment for testing
  3. a *team of developers*, responsible of the design and implementation of the
     desired features in the product

In order to have more realistic examples, lets suppose following facts:

  1. the maintainer username is `rocher` (it's the GitHub username I'm using to
     develop and maintain this tutorial; change it for `lee`, if you feel more
     comfortable)
  2. the integrator username is `ted`
  3. in the developers team we have `alice` and `bob`
  4. GitHub repository is used as a central, distribution point, so only
     `master`, `develop` and `support/*` branches should be there
  5. `feature/*` branches might be in GitHub when some team member must publish
     a feature branch
  6. software development, integration, testing and release takes place locally,
     so there is no need that neither `release/*` nor `hotfix/*` branches to be
     in GitHub



## Creating a new repository
GitHub repository owner creates a new repository on github, and clone it locally:

```{shell}
rocher$ git clone git@github.com:rocher/foobar-origin.git foobar
Cloning into 'foobar'...
warning: You appear to have cloned an empty repository.

rocher$ cd foobar
r/foobar (master)$ git flow init -d
Using default branch names.
No branches exist yet. Base branches must be created now.
Branch name for production releases: [master]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Bugfix branches? [bugfix/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []
Hooks and filters directory? [rocher/foobar/.git/hooks]

r/foobar (develop)$
```
