---
layout: default
title: PM2
description: Deployment of a skulljs project with pm2.
parent: Deployment
last_modified_date: 2022-11-18 12:09
---

# Deployment with PM2
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
- Latest LTS of [Node.js](https://nodejs.org/en/) on the remote server and on the local computer
- [skulljs-cli](https://www.npmjs.com/package/@skulljs/cli) globally installed on the local computer
- [PM2](https://pm2.keymetrics.io/docs/usage/pm2-doc-single-page/) globally installed on the remote server
- MySQL installed on the remote server
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
1. Select PM2 when the CLI ask for manager

---

## Step 3 - Setup the folder on the remote server

1. Create a folder with the name of your choice in your server. Ex: my-awesome-app
1. Copy the dist folder in that folder
1. Install the dependencies with the following command

{% highlight bash %}
$ npm install
{% endhighlight %}

## Step 4 - Initialize the database on the remote server

1. Change the database configuration in the .env file
1. Init the database (depends of the ORM in use, check examples below)

### Ex: Prisma

{% highlight bash %}
<!-- Classic -->
$ npx prisma db push
$ npx prisma db seed
or
<!-- With migration -->
$ npx prisma migrate reset
or
<!-- Only migrate change -->
$ npx prisma migrate deploy
{% endhighlight %}

## Step 5 - Use PM2

The last step of the deployment is to setup PM2. We use PM2 to manage and keep our application online 24/7.

### Start an app

In the dist folder, use the following command.

{% highlight bash %}
$ npm run pm2:start
{% endhighlight %}

### Managing process

You can use the following commands to manage your processes

{% highlight bash %}
$ npm run pm2:start
$ npm run pm2:stop
$ npm run pm2:restart
$ npm run pm2:reload
$ npm run pm2:delete
$ npm run pm2:logs
{% endhighlight %}

### Setup startup script

This step will allow you to restart PM2 with the processes it manage when the server boot/reboot.

You can use the following commands for that.

{% highlight bash %}
$ npm run pm2:startup
$ npm run pm2:save
{% endhighlight %}

## Step 6 - Go to the app

Well done ! Your app is now deployed and available at:

{% highlight url %}
http(s)://[the name or the ip of the server]:[port of the server]
{% endhighlight %}
