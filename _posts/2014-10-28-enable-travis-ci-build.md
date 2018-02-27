---
layout: post
title: Enabling Travis-CI build on Github-Pages site
categories: build
description: How to set up a continuous build for your Github pages repo to do basic testing.
---

Sign up for [Travis-CI](https://travis-ci.org)

Go to https://travis-ci.org/profile/#yourname# and turn CI on for your repo.

Return to your Github pages repo and add a Gemfile including gihub-pages and html-proofer:

{% gist 54b62bb34dfba66cac23 %}

Add a .travis.yml file to build your Jekyll site and run htmlproofer against the generated content:

{% gist 78705cfd742e684bc113 %}

Edit your readme.md to include the build status image:

    ![build status](https://travis-ci.org/sihugh/sihugh.github.io.svg)

Commit and push

... Wait for the build failure email telling you about the broken links on your sites... :-D
