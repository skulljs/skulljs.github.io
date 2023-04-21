---
title: "Quick Start"
description: "Follow these instructions to create a new Skulljs project."
lead: "Follow these instructions to create a new Skulljs project."
date: 2023-04-19T13:57:29+02:00
lastmod: 2023-04-19T13:57:29+02:00
draft: false
images: []
menu:
  docs:
    parent: "overview"
weight: 120
toc: true
---

## Requirements

- [Git](https://git-scm.com/) — latest source release
- [Node.js](https://nodejs.org/) — latest LTS version or newer
- [MySQL](https://www.mysql.com/) — 8.0 version or newer

{{< details "Why Git?" >}}
Skulljs uses git [repositories](https://github.com/skulljs) to generate the project structure.
{{< /details >}}

## Start a new Skulljs project

{{< alert icon="👉" >}}
In this example we will use the _angular_ and _nestjs_ components of Skulljs
{{< /alert >}}

Install the CLI, create a new project, modify the backend configuration, configure database access, initialize the database, and start the app.

### Install the CLI

We have created a CLI named skulljs-cli to simplify the usage of Skulljs as much as possible.

```bash
npm install --global @skulljs/cli
```

### Create a new project

```bash
sk new <project_name>
```

When prompted:

{{< alert icon="👉" >}}
Select _angular_ and _nestjs_
{{< /alert >}}

### Modify the backend configuration

{{< alert icon="⚠️" >}}
For security purposes you need to modify the configuration located in backend/src/configs/configuration.ts
{{< /alert >}}

```typescript
// backend/src/configs/configuration.ts
export const configuration = () => ({
  // Api

  // general prefix for nestjs routes
  apiPrefix: "api",
  // nestjs port
  port: 3000,

  // Access Logger

  // the max size of the file before it rotates
  accessLoggerFileSize: "10M",
  // the max time before it rotates
  accessLoggerFileInterval: "1d",

  // Helmet

  // false for sk build
  helmetContentSecurityPolicy: false,

  // Cors

  // allowed origins | Ex: angular
  corsOrigins: ["http://localhost:4200"],

  // OpenApi

  // path of the open api docs
  openAPIPath: "api",
  // title of the open api docs
  openAPITitle: "skulljs nestjs example",
  // description of the open api docs
  openAPIDescription: "nestjs component for skulljs",
  // version of the open api docs
  openAPIVersion: "1.0",

  // Session

  // ! you need to change this
  sessionSecret: "changeMeOrInsecure",
  // value in ms | 1 day
  sessionCookieMaxAge: 86400000,
  // true = Forces the session to be saved back to the session store, even if the session was never modified during the request.
  sessionResave: false,
  // true = Forces a session that is "uninitialized" to be saved to the store. A session is uninitialized when it is new but not modified.
  sessionSaveUninitialized: false,
  // Specifies the boolean value for the HttpOnly Set-Cookie attribute.
  sessionCookieHttpOnly: false,
  // Specifies the boolean value for the Secure Set-Cookie attribute.
  sessionCookieSecure: "auto",

  // Mailer

  // Smtp Host
  mailerSmtpHost: "smtp.example.com",
  // Smtp Port
  mailerSmtpPort: 25,
  // Default from for mails
  mailerDefaultFrom: '"skulljs" <skulljs@example.com>',

  // Crypto

  // ! you need to change this, === 32 characters
  cryptoSecretKey: "changeMeOrInsecure".padEnd(32, "!"),
});
```

### Configure database access

```bash
# ./backend/.env
DATABASE_URL="mysql://username:password@127.0.0.1:3306/skulljs"
```

### Initialize the database

{{< alert icon="👉" >}}
Requires to be in backend folder
{{< /alert >}}

```bash
npx prisma db push
npx prisma db seed
```

### Run the app

#### nestjs

{{< alert icon="👉" >}}
In backend folder
{{< /alert >}}

```bash
npm run start:dev
```

Skulljs will start the angular development webserver accessible by default at `http://localhost:3000`. Saved changes will live reload in the browser.

#### angular

{{< alert icon="👉" >}}
In frontend folder
{{< /alert >}}

```bash
npm run start
```

Skulljs will start the angular development webserver accessible by default at `http://localhost:4200`. Saved changes will live reload in the browser.

## Other commands

Skulljs comes with commands for common tasks. [Commands →]({{< relref "commands" >}})

## Features

Skulljs comes with many features. [Features →]({{< relref "features" >}})
