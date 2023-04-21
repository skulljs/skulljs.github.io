---
title: "Docker Deployment"
description: "Follow these instructions to to deploy a Skulljs project with Docker."
lead: "Follow these instructions to to deploy a Skulljs project with Docker."
date: 2023-04-19T15:54:29+02:00
lastmod: 2023-04-19T15:54:29+02:00
draft: false
images: []
menu:
  docs:
    how-to:
      parent: "deployment"
weight: 291
toc: true
---

## Requirements

- Working project — check that your project works locally
- [Node.js](https://nodejs.org/) on local computer — latest LTS version or newer
- [Skulljs-cli](https://www.npmjs.com/package/@skulljs/cli) on local computer — the version you used to create the project or a newer version
- [Docker](https://docs.docker.com/engine/install/) and [Docker Compose](https://docs.docker.com/compose/install/) installed on the remote server — the latest LTS
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
1. Select DOCKER when the CLI prompts you to select a manager

### Setup the folder on the remote server

1. Create a folder with the name of your choice in your server. Ex: my-awesome-app
1. Copy the dist folder in that folder
1. Edit the database config in **.env** and **docker-compose.yml**

{{< alert icon="👉" >}}
The database hostname in .env is the service name in docker compose. Ex: database\_<project_name>.
{{< /alert >}}

```yaml
- MYSQL_ROOT_USER=root
- MYSQL_ROOT_PASSWORD=
- MYSQL_USER=
- MYSQL_PASSWORD=
- MYSQL_DATABASE=
```

### Use Docker

We use docker to manage and keep our application online 24/7.

#### Start an app

In the dist folder, use the following command.

```bash
npm run docker:up
```

#### Managing process

You can use the following commands to manage your processes.

```bash
npm run docker:build
npm run docker:up
npm run docker:down
npm run docker:logs
```

### Initialize the database in the docker container

1. Wait for the docker containers to boot up
   {{< alert icon="👉" >}}
   This can take up to 5min, execute 'npm run docker:logs' once this delay has passed.
   {{< /alert >}}
1. Init the database
   {{< alert icon="👉" >}}
   Actions may vary depending on the ORM being used. Please see below for examples.
   {{< /alert >}}

#### Ex: Prisma

```bash
# Enter docker container
docker compose exec <app_name> bash

# Classic
npx prisma db push
npx prisma db seed
or
# With migration
npx prisma migrate deploy
npx prisma db seed

# Exit docker container
exit
```

### Go to the app

Well done ! Your app is now deployed and available at:

```url
http(s)://[the name or the ip of the server]:[port of the server]
```

## Troubleshooting

### Permissions problem

Please manually create the folder used in Docker volumes and ensure that it has appropriate permissions.
