---
title: "PM2 Deployment"
description: "Follow these instructions to to deploy a Skulljs project with PM2."
lead: "Follow these instructions to to deploy a Skulljs project with PM2."
date: 2023-04-19T15:54:29+02:00
lastmod: 2023-04-19T15:54:29+02:00
draft: false
images: []
menu:
  docs:
    how-to:
      parent: "deployment"
weight: 292
toc: true
---

## Requirements

- Working project — check that your project works locally
- [Node.js](https://nodejs.org/) on local computer and remote server — latest LTS version or newer
- [Skulljs-cli](https://www.npmjs.com/package/@skulljs/cli) on local computer — the version you used to create the project or a newer version
- [PM2](https://pm2.keymetrics.io/docs/usage/pm2-doc-single-page/) globally installed on the remote server — latest LTS
- [MySQL](https://www.mysql.com/) on remote server — 8.0 version or newer
- (Optional: HTTPS) An SSL Certificate

## Deploy your app

Set up SSL certificate

### (Optional) Set up SSL certificate for HTTPS

1. Put your certificate key in **sslcert/xxx.key.pem**, you are only able to rename the **xxx** part.
1. Put your certificate file in **sslcert/xxx.cert.pem**, you are only able to rename the **xxx** part.

### Build the project

```bash
sk build
```

1. Enter the name of the app
1. Enter the ip address or the name of the remote server where you wish to deploy your application.
   {{< alert icon="👉" >}}
   We recommend to enter the name rather than the ip address to make sure you don't encounter problems with certificates.
   {{< /alert >}}
1. Enter the port of the remote server where you wish to deploy your application.
1. Select which hypertext transfer protocol do you would like to use.
   {{< alert icon="👉" >}}
   Selecting HTTPS requires you to make the optional step. This is recommended.
   {{< /alert >}}
1. Select PM2 when the CLI prompts you to select a manager

### Setup the folder on the remote server

1. Create a folder with the name of your choice in your server. Ex: my-awesome-app
1. Copy the dist folder in that folder
1. Install the dependencies with the following command

```bash
npm install
```

### Initialize the database on the remote server

1. Change the database configuration in the .env file
1. Init the database
   {{< alert icon="👉" >}}
   Actions may vary depending on the ORM being used. Please see below for examples.
   {{< /alert >}}

#### Ex: Prisma

```bash
# Classic
npx prisma db push
npx prisma db seed
or
# With migration
npx prisma migrate deploy
npx prisma db seed
```

### Use PM2

The last step of the deployment is to setup PM2. We use PM2 to manage and keep our application online 24/7.

#### Start an app

In the dist folder, use the following command.

```bash
npm run pm2:start
```

#### Managing process

You can use the following commands to manage your processes.

```bash
npm run pm2:start
npm run pm2:stop
npm run pm2:restart
npm run pm2:reload
npm run pm2:delete
npm run pm2:logs
```

### Go to the app

Well done ! Your app is now deployed and available at:

```url
http(s)://[the name or the ip of the server]:[port of the server]
```
