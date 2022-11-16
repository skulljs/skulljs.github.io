---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Getting started
description: Quick install guide for testing the skulljs project. Test it now !
last_modified_date: 2022-11-16 16:40
nav_order: 2
---

# Getting started

This page aims to give a quick install guide for testing the skulljs project.
{: .fs-6 .fw-300 }

---

## Prerequisities

- Latest LTS of [Node.js](https://nodejs.org/en/)
- [MySQL](https://www.mysql.com/fr/) installed

---

1- Install the kestrel-cli
{% highlight bash %}
$ npm install --global @skulljs/cli
{% endhighlight %}

2- Create a new project
{% highlight bash %}
$ sk new <project_name>
{% endhighlight %}

3- Configure the database access in **backend/.env**
{% highlight env %}
DATABASE_URL="mysql://username:password@127.0.0.1:3306/skulljs"
{% endhighlight %}

4- Initialize the database (in backend folder)
{% highlight bash %}
$ npx prisma db push
$ npx prisma db seed
{% endhighlight %}

5- Running the app (in backend and frontend folder)
{% highlight bash %}
$ npm start
{% endhighlight %}

6- Point your web browser to [http://localhost:4200](http://localhost:4200).

By default you can access the _backend_ on [http://localhost:3000](http://localhost:3000) and the _frontend_ on [http://localhost:4200](http://localhost:4200).

The _API documentation_ can be accessed on [http://localhost:3000/api](http://localhost:3000/api).
