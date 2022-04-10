---
layout: post
title: "Useful Git Commands"
date: 2022-04-11 01:53:00 +0300
author: semih
comments: true
lang: en
lang-ref: useful-git-commands
categories: [Git]
tags: [git, version-control]
published: true
---
development is your working branch

```bash
- git pull // gets last updates from your branch
- git checkout BRANCH_NAME // changes your working branch
- git checkout -D BRANCH_NAME // deletes your branch both in local and remote environments
- git checkout -b development // creates a branch based on development
- git switch -c BRANCH_NAME // switches your branch and your changes
- git rebase development // updates your branch with your last changes of the based branch

- git add FILE_NAME // adds your file to stage area
- git commit -m "YOUR_COMMENT" // commit your file with YOUR_COMMENT
```