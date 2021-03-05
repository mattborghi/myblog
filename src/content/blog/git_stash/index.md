---
layout: post
title: Working with Git Stash
image: ../../img/github.jpg
author: [Matias Borghi]
date: 2020-10-14T08:18:03.284Z
excerpt: Quick memo showing how to work with git stash
tags: ['Github']
---

## Using Git Stash

The utility for git stash, in my case, comes from needing to change branches and having files not staged that I don't want to commit yet.

So, my workflow in this case is to:

```shell
git stash push -m " write a descriptive message"
```

We can check all the staged instances as follows:

```shell
git stash list

stash@{0}: On branch-name: message 1
stash@{1}: On another-branch: message 2
```

Now that the directory is clean we can change branches, make the necessary changes there and return to our previous branch.

There, we can recover the state of our work being stashed. Let's say that we want to recover the ``stash@{n}``.

```shell
git stash apply --index n
```
That's it!. But wait, we should still have our stashed info when we list it. In order to remove it we can do

```shell
git stash drop stash@{0}

git stash list

stash@{1}: On another-branch: message 2
```

and we will see only the relevant stash data.

One way to do this two steps in one: ``apply + drop`` is to use 

```shell
git stash pop --index n
```

