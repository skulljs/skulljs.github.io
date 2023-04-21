---
title: "File structure"
description: "Here is the file structure of a Skulljs project."
lead: "Here is the file structure of a Skulljs project."
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

It contains the selected backend component of Skulljs. (Ex: nestjs)

### Frontend

It contains the selected frontend component of Skulljs. (Ex: angular)

### sslcert

It contains the key and the certificate for the deployment of the app.

## Root files

### .editorconfig

Configuration file for [EditorConfig](https://editorconfig.org/). It allows you to maintain consistent coding styles throughout your projects.

### .gitignore

Configuration file that specifies which files Git should ignore.

### .prettierrc

Configuration file for [Prettier](https://prettier.io/). It allows you to format your code to keep it coherent.

### .skulljs-cli.json

Meta file for Skulljs.
