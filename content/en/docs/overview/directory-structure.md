---
title: "Directory structure"
description: "Here is the directory structure of a Skulljs project."
lead: "Here is the directory structure of a Skulljs project."
date: 2023-04-19T15:04:29+02:00
lastmod: 2023-04-19T15:04:29+02:00
draft: false
images: []
menu:
  docs:
    parent: "overview"
weight: 140
toc: true
---

```bash
.
├── backend/
├── frontend/
├── sslcert/
├── .editorconfig
├── .gitignore
├── .prettierrc
├── .skulljs-cli.json
```

## Root directories

### Backend

It contains the selected backend Skulljs's component. (Ex: nestjs)

### Frontend

It contains the selected frontend Skulljs's component. (Ex: angular)

### sslcert

It contains the key and the certificate for the deployment of the app.

## Root files

### .editorconfig

Configuration file for [EditorConfig](https://editorconfig.org/). It allow you to maintain consistent coding styles for your projects.

### .gitignore

Configuration file that specifies which files Git should disregard.

### .prettierrc

Configuration file for [Prettier](https://prettier.io/). It enables you to format your code to keep it coherent.

### .skulljs-cli.json

Meta file for Skulljs.
