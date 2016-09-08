---
layout: page
title: README
author: The Nerdery Ruby Standards Task Force
---

# Introduction

This small Jekyll-based site houses the Ruby Standards used by developers at The Nerdery.  If you're a Nerdery developer, you should totally know these standards by heart.  If not?  This is a great place to learn some (at least we think) awesome best practices.

# Contributing

There's two ways you can contribute to this repository:

1. Get access from @sumpygump, create a branch and issue a [Pull Request](https://github.com/blog/1943-how-to-write-the-perfect-pull-request).
1. Make a fork and then issue a [Pull Request](https://github.com/blog/1943-how-to-write-the-perfect-pull-request)

We can actually discuss your PR and decide if we want to pull it into our main standards or not, so **don't be shy**.

# Project Structure

```
  |
  |- index.md              - the main standards document
  |- _sass                 - where the sass lives
  |- _layouts/default.html - the main page wrapper
  |- _layouts/page.html    - the main layout for the standards document
```

# Getting Started


You will need Ruby installed and properly functioning for this Jekyll site to run locally.  If you don't already, you can certainly [consult this guide](http://somewhere.com/#installing-ruby) to get it installed properly.

```sh
bundle install
bundle exec jekyll serve
```

After that, the site will be running @ http://localhost:4000 and sports live-reloading as you make changes.
