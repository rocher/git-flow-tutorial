<!--*- mardown-mode, auto-fill, flyspell -*-->
<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-generate-toc again -->
**Table of Contents**

- [(*wip*) GitHub + git-flow Tutorial](#wip-github--git-flow-tutorial)
    - [Introduction](#introduction)
        - [Tutorial context](#tutorial-context)
        - [Examples](#examples)
    - [Create the main repository](#create-the-main-repository)
        - [Clone locally](#clone-locally)
        - [Initialize git-flow](#initialize-git-flow)
        - [Synchronize initialization](#synchronize-initialization)
    - [Start working on features](#start-working-on-features)
        - [Initial cloning](#initial-cloning)
        - [Creating a new feature branch](#creating-a-new-feature-branch)

<!-- markdown-toc end -->

# (*wip*) GitHub + git-flow Tutorial

## Introduction
This tutorial shows how to use GitHub and [git-flow] together.

To show in detail the use of git-flow, this tutorial is developed around an
imaginary open-source project called `foobar`, developed by a team of software
developers. The same works for a private, closed software project, and for
projects with a different role assignment or software development methodologies.

### Tutorial context
In the context of this tutorial, the following actors are supposed to exist and
to actively participate in some part of the software development cycle:

  1. a *maintainer*, responsible to announce, publish and release new versions,
     make hot fixes and give support to old releases
  2. an *integrator*, responsible of the continuous integration of the features
     the team is producing and to provide a suitable environment for testing
  3. a *team of developers*, responsible of the design and implementation of the
     desired features in the product

### Examples
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

## Create the main repository
When starting from scratch, the very first thing to do is to create a new GitHub
repository. Please check [GitHub documentation][1] on how to do this.

In this tutorial, the project is called `foobar`, so the main repository is
named `foobar-origin` to emphasize that this is the main public reference of the
project, where versions are released, contributors can send pull requests and
and package integrator can download the source code.

Once created, the maintainer makes a local copy in order to initialize
`git-flow`.

### Clone locally
```{shell}
[1] rocher> git clone git@github.com:rocher/foobar-origin.git foobar
Cloning into 'foobar'...
warning: You appear to have cloned an empty repository.

[-] rocher>
```

### Initialize git-flow
```shell
[1] rocher> cd foobar

[2] r/foobar (master)> git flow init -d
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

### Synchronize initialization
At this point, local `foobar` has two branches but no files, so it is better to
start with simple, common files:

```shell
[1] r/foobar (develop)> emacs README.md .gitignore
    [ write some initial description in README.md and files to be ignored in .gitignore ]

[2] r/foobar (develop)> git add README.md .gitignore

[3] r/foobar (develop)> git commit -m 'Add basic files'
[develop 3eb00b8] Add basic files
 2 files changed, 3 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 README.md

[4] r/foobar (develop)> git push origin develop
Counting objects: 6, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 500 bytes | 0 bytes/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To github.com:rocher/foobar-origin.git
 * [new branch]      develop -> develop

[-] r/foobar (develop)>
```

Note that the `master` branch has not been created in `foobar-origin`, but who
cares? There are no releases to publish, so it is not needed at all.

## Start working on features
Ok, at this point your team is ready to implement cool features. The main idea
is that each developer works locally on a feature, individually or in
collaboration with other members.

### Initial cloning
Alice and Bob start by creating their local copies of `foobar-origin`
repository. The example below shows how Alice would proceed, but the same
applies to Bob:

```shell
[1] alice> git clone git@github.com:rocher/foobar-origin.git foobar
Cloning into 'foobar'...
remote: Counting objects: 6, done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 6 (delta 0), reused 6 (delta 0), pack-reused 0
Receiving objects: 100% (6/6), done.
warning: remote HEAD refers to nonexistent ref, unable to checkout.

[2] alice> cd foobar

[3] a/foobar (master)> git flow init -d
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
Hooks and filters directory? [alice/foobar/.git/hooks]

[4] a/foobar (develop)> branch
* develop
  master

[5] a/foobar (develop)> ls -a1
total 20
./
../
.git/
.gitignore
README.md

[-] a/foobar (develop)>
```

### Creating a new feature branch
Once the local repository has been cloned from `foobar-origin` and
*git-flow-initialized*, it's time to create the first feature branch:

```shell
[1] a/foobar (develop)> git flow feature start analytic-algorithm
Switched to a new branch 'feature/analytic-algorithm'

Summary of actions:
- A new branch 'feature/analytic-algorithm' was created, based on 'develop'
- You are now on branch 'feature/analytic-algorithm'

Now, start committing on your feature. When done, use:

     git flow feature finish analytic-algorithm

[-] a/foobar (feature/analytic-algorithm)>
```

Feature branches can be used (but you're not advised to do) as a kind of
*backup* branches. The question is that

  > if only one developer is working on a feature branch, then all commits can be
  > safely pushed, even when compilation fails or something else is broken.

That's completely false for other branches, or for feature branches shared
between team members. So please make sure how you use feature branches.


[git-flow]: https://github.com/petervanderdoes/gitflow-avh
[1]: https://help.github.com/articles/create-a-repo
