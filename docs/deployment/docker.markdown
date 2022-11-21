---
layout: default
title: Docker
description: Deployment of a skulljs project with docker.
parent: Deployment
last_modified_date: 2022-11-18 12:09
---

# Deployment with Docker
{: .no_toc }

When you are ready to deploy your application to a remote server, you can follow this guide.
{: .fs-6 .fw-300 }

---

## Table of contents
{: .no_toc  .text-delta }

1. TOC
{:toc}

---

## Step 1 - Install the prerequisities

- Verify that your project work in development
- Latest LTS of [Node.js](https://nodejs.org/en/) on the local computer
- [skulljs-cli](https://www.npmjs.com/package/@skulljs/cli) globally installed on the local computer
- [Docker](https://docs.docker.com/engine/install/) and [Docker Compose](https://docs.docker.com/compose/install/) installed on the remote server
- (Optional: HTTPS) An SSL Certificate

---

## Optional step - Set up SSL certificate for HTTPS

1. Put your certificate key in **sslcert/xxx.key.pem**, you can only change the xxx part
1. Put your certificate file in **sslcert/xxx.cert.pem**, you can only change the xxx part

---

## Step 2 - Build the project

{% highlight bash %}
$ sk build
{% endhighlight %}

1. Enter the name of the app
1. Enter the ip or the name of the remote server which you want to deploy your app
1. Enter the port of the remote server which you want to deploy your app
1. Select which hypertext transfer protocol do you want to use (select https require the previous step)
1. Select DOCKER when the CLI ask for manager

---

## Step 3 - Setup the folder on the remote server

1. Create a folder with the name of your choice in your server. Ex: my-awesome-app
1. Copy the dist folder in that folder
1. Edit database config in **.env** and **docker-compose.yml** (the database hostname in .env is the service name in compose: mysql)

{% highlight yaml %}
- MYSQL_ROOT_USER=root
- MYSQL_ROOT_PASSWORD=
- MYSQL_USER=
- MYSQL_PASSWORD=
- MYSQL_DATABASE=
{% endhighlight %}

## Step 4 - Use docker

We use docker to manage and keep our application online 24/7.

### Start an app

In the dist folder, use the following command.

{% highlight bash %}
$ npm run docker:up
{% endhighlight %}

### Managing process

You can use the following commands to manage your processes

{% highlight bash %}
$ npm run docker:build
$ npm run docker:up
$ npm run docker:down
$ npm run docker:logs
{% endhighlight %}

## Step 5 - Initialize the database in the docker container

1. Init the database (depends of the ORM in use, check examples below)

### Ex: Prisma

{% highlight bash %}
<!-- Enter docker container -->
$ docker compose exec <app_name> bash

<!-- Classic -->
$ npx prisma db push
$ npx prisma db seed
or
<!-- With migration -->
$ npx prisma migrate reset
or
<!-- Only migrate change -->
$ npx prisma migrate deploy

<!-- Exit docker container -->
$ exit
{% endhighlight %}

## Step 6 - Go to the app

Well done ! Your app is now deployed and available at:

{% highlight url %}
http(s)://[the name or the ip of the server]:[port of the server]
{% endhighlight %}
