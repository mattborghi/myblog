---
layout: post
title: "ROS Expire Signatures"
image: ../../img/ros.png
author: [Matias Borghi]
date: 2021-11-17
excerpt: Just a memo for revalidating expiring signatures in ROS.
tags: ['ROS']
---

# ROS expired signatures

Solving the issue of ROS expiring signatures in Ubuntu is as easy as typing this command in the terminal:

```
curl http://repo.ros2.org/repos.key | sudo apt-key add -
```