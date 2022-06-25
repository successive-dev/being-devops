---
title: "implement versioning in cicd pipeline"
date: 2022-06-20T21:00:32+05:30
publishdate: 2022-06-20
lastmod: 2022-06-20
draft: false
tags: ["semver", "semantic-versioning", "cicd", "pipeline", "git"]
---

This is the tool which we are going to use \- [https://github.com/screwdriver\-cd/gitversion](https://github.com/screwdriver-cd/gitversion). Binary of the tool can be downloaded from releases page in the repo. 

This is a very simpleton tool \- what it does is reads the current git tag \(locally from .git folder, and yes it obviously works with git\) and can bump the major, minor or patch bit of the tag based on the last commit message. Please read about semantic versioning document if major, minor and patch doesn't make. This doesn't strictly follow semantic versioning rules but yeah it works on tag with format \- [xxx.xxx.xxx](http://xxx.xxx.xxx)

I'm using this tool for all my cicd projects and the flow with this tool is very simple. It's mostly just two commands.

```
./gitversion bump auto // automatically bumps the tag (it also runs git tag command in background)
git push --tags
```

Alternatively we can also export the tag in environment variable or in a file to reference the tag at any later stage in pipeline.
