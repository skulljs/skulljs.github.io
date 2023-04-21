---
title: "Quick Start"
description: "One page summary of how to start a new Skulljs project."
lead: "One page summary of how to start a new Skulljs project."
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
In this example we will use the _angular_ and the _nestjs_ components of Skulljs
{{< /alert >}}

Install the CLI, create a new project, change the backend configuration, configure the database access, initialize the database, and start the app.

### Install the CLI

To make it as easy as possible to use Skulljs, we made a CLI named skulljs-cli.

```bash
npm install --global @skulljs/cli
```

### Create a new project

```bash
sk new <project_name>
```

When prompted:

{{< alert icon="👉" >}}
Select _angular_  and _nestjs_
{{< /alert >}}

### Change the backend configuration

{{< alert icon="🛑" >}}
For security purpose you need to change the configuration located in backend/src/configs/configuration.ts
{{< /alert >}}

```typescript
// backend/src/configs/configuration.ts
export const configuration = () => ({
  // Api
  apiPrefix: 'api', // general prefix for nestjs routes
  port: 3000, // nestjs port

  // Access Logger
  accessLoggerFileSize: '10M', // the max size of the file before it rotates
  accessLoggerFileInterval: '1d', // the max time before it rotates

  // Helmet
  helmetContentSecurityPolicy: false, // false for sk build

  // Cors
  corsOrigins: ['http://localhost:4200'], // allowed origins | Ex: angular

  // OpenAPI
  openAPIPath: 'api', // path of the open api docs
  openAPITitle: 'skulljs nestjs example', // title of the open api docs
  openAPIDescription: 'nestjs component for skulljs', // description of the open api docs
  openAPIVersion: '1.0', // version of the open api docs

  // Session
  sessionSecret: 'changeMeOrInsecure', // ! you need to change this
  sessionCookieMaxAge: 86400000, // value in ms | 1 day
  sessionResave: false, // true = Forces the session to be saved back to the session store, even if the session was never modified during the request.
  sessionSaveUninitialized: false, // true = Forces a session that is "uninitialized" to be saved to the store. A session is uninitialized when it is new but not modified.
  sessionCookieHttpOnly: false, // Specifies the boolean value for the HttpOnly Set-Cookie attribute.
  sessionCookieSecure: 'auto', // Specifies the boolean value for the Secure Set-Cookie attribute.

  // Mailer
  mailerSmtpHost: 'smtp.example.com', // Smtp Host
  mailerSmtpPort: 25, // Smtp Port
  mailerDefaultFrom: '"skulljs" <skulljs@example.com>', // Default from for mails

  // Crypto
  cryptoSecretKey: 'changeMeOrInsecure'.padEnd(32, '!'), // ! you need to change this, === 32 characters
});
```

### Configure the database access

```bash
# ./backend/.env
DATABASE_URL="mysql://username:password@127.0.0.1:3306/skulljs"
```

### Initialize the database

{{< alert icon="👉" >}}
Require to be in backend folder
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

Skulljs comes with many features.  [Features →]({{< relref "features" >}})
