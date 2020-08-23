---
layout: post
title: Github Pages
image: ./github.png
author: [Matias Borghi]
date: 2019-08-08T00:54:03.284Z
excerpt: In this post I describe how I implement Github pages and Gatsby.
tags: ['Tech']
---

Basically the source code is in the [current repo](https://github.com/mattborghi/website-source), named `website-source`, whereas the built Gatsby blog is located in `https://github.com/mattborghi/mattborghi.github.io`. Which is deployed in the page you are currently seen (https://mattborghi.github.io).

Following the instructions from the [Gatsby page](https://www.gatsbyjs.org/docs/how-gatsby-works-with-github-pages/) and a Github conversation (I don't have the link) I found out how to push the results from the source file into our github pages `<repo>`.

Basically, we have to install `github-pages` and add the following script into the `package.json` file:

```json
"deploy": "gatsby build 
            && npx gh-pages 
                --git git 
                -d public -b master 
                -r https://github.com/mattborghi/mattborghi.github.io"
```
