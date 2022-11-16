---
layout: default
title: Deployment
description: Quick guide for deploy your application on a remote server for production purpose
last_modified_date: 2022-08-29 15:29
nav_order: 4
---

# Deployment
{: .no_toc }

When you are ready to deploy your application to a remote server, you can follow this guide.
{: .fs-6 .fw-300 }

---

## Table of contents
{: .no_toc  .text-delta }

1. TOC
{:toc}

---

<!-- ## Step 1 - Install the prerequisities

- Verify that your project work in development
- Latest LTS of [Node.js](https://nodejs.org/en/) on the remote server and on the local computer
- [Nodemon](https://www.npmjs.com/package/nodemon) globally installed on the remote server and on the local computer
- [kestrel-cli](https://www.npmjs.com/package/@kestrels/cli) globally installed on the remote server and on the local computer
- Any kind of database on the remote server (use the same as you used in development is a plus)
- [PM2](https://pm2.keymetrics.io/docs/usage/pm2-doc-single-page/) installed on the remote server
- An SSL Certificate

---

## Step 2 - Build the project

{% highlight bash %}
$ kc build
{% endhighlight %}

1. Select yes when the cli ask you to modify the cors config
1. Enter the ip or the name of the remote server which you want to deploy your app

---

## Step 3 - Setup the folder on the remote server

1. Create a folder with the name of your choice. Ex: my-awesome-app
1. Copy the dist folder in that folder. (you can remove the node_modules folder and reinstall the modules after the copy if you want the process to be faster)
1. Copy the sslcert folder in the folder created in 1
1. Replace the files in the sslcert folder with your SSL certificate
1. Verify that the path in server.js correctly refer to the files in the sslcert folder

## Step 4 - Setup the kestrel-cli file on the remote server

1. Make a file in the folder created in the previous step named "kestrel-cli.json"

{% highlight json %}
{
  "projects" : {
    "backend_path" : "dist",
    "frontend_path" : "dist"
  },
  "version" : "3.0.0"
}
{% endhighlight %}

## Step 5 - Initialize the database on the remote server

1. Change the prod database configuration in the .env file
1. Run the following command

{% highlight bash %}
$ kc idb
{% endhighlight %}

You can now test your app by typing using npm start in the dist folder. The URL is https://[the name or the ip of the server].

## Step 6 - Use PM2

The last step of the deployment is to setup PM2. We use PM2 to manage and keep our application online 24/7.

### Start an app

In the dist folder, use the following command.

{% highlight bash %}
$ pm2 start src/server.js --name <name of the app>
{% endhighlight %}

### Managing process

You can use the following commands to manage your processes

{% highlight bash %}
$ pm2 restart <name of the app>
$ pm2 reload <name of the app>
$ pm2 stop <name of the app>
$ pm2 delete <name of the app>
$ pm2 list
$ pm2 logs
{% endhighlight %}

### Setup startup script

This step will allow you to restart PM2 with the processes it manage when the server boot/reboot.

You can use the following commands for that.

{% highlight bash %}
$ pm2 startup
$ pm2 save
{% endhighlight %}

## Step 7 - Go to the app

Well done ! Your app is now deployed and available at https://[the name or the ip of the server] -->
