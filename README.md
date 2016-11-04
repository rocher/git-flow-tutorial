<!--*- mardown-mode, auto-fill, flyspell -*-->

# [ *work in progress* ]

<span style="size:38px">Hello, world</span>

---

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-generate-toc again -->
**Table of Contents**

- [[ *work in progress* ]](#-work-in-progress-)
- [GitHub + git-flow Tutorial](#github--git-flow-tutorial)
    - [Introduction](#introduction)
    - [Creating a new repository](#creating-a-new-repository)

<!-- markdown-toc end -->

# GitHub + git-flow Tutorial

## Introduction
This tutorial shows how to use GitHub and [git-flow] together.

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
  7. the *shell* examples are written in a `fish`*-like* look & feel:
     * the prompt shows only the path, with abbreviated parent directories
     * the root path is the same as the username, so `ted>` indicates the home
       directory of `ted`
     * when in a git repository, the current checked out branch is shown in
       parenthesis, so `t/example (master)>` indicates that `ted` is currently
       in the directory `example`, which is a git repository, being `master` the
       currently checked out branch
     * there is an number at the beginning of each issued command
     * blocks of commands and their respective output are separated by a blank
       line
     * examples end with a single prompt

     example:
     ```shell
     [1] ted> git init example
     Initialized empty Git repository in ted/example/.git/

     [2] ted> cd example

     [3] t/example (master)> branch
     * master

     [-] t/example (master)>
     ```



## Creating a new repository
The very first thing to do, when starting from scratch, is to create a new
GitHub repository. Please
check [GitHub documentation][1] on
how to do this

```{shell}
[1] rocher> git clone git@github.com:rocher/foobar-origin.git foobar
Cloning into 'foobar'...
warning: You appear to have cloned an empty repository.

[2] rocher> cd foobar

[3] r/foobar (master)> git flow init -d
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

[-] r/foobar (develop)>
```


[git-flow]: https://github.com/petervanderdoes/gitflow-avh
[1]: https://help.github.com/articles/create-a-repo
