---
title: "Troubleshooting"
description: "Solutions to common problems."
lead: "Solutions to common problems."
date: 2023-04-21T16:46:29+02:00
lastmod: 2023-04-21T16:46:29+02:00
draft: false
images: []
menu:
  docs:
    parent: "help"
weight: 410
toc: true
---

## Problems updating npm packages

Delete the `./node_modules` folder then run:

```bash
npm install
```

## Problems with cache

Delete the temporary directories:

- dist for NestJs

## CORS Problems

Add your frontend base url to the backend whitelist.

## Permissions problem

Please manually create the folder used in Docker volumes and ensure that it has appropriate permissions.
