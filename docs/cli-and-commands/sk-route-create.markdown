---
layout: default
title: sk route:create
description: Description of the sk route:create command
parent: CLI and commands
last_modified_date: 2022-11-16 16:55
---

# sk route:create

## Feature

Create a new route for the backend repository and a new service for the frontend repository based on user answers

## Usage

{% highlight bash %}
$ sk route:create <route-path> [options]
$ sk rc <route-path> [options]
{% endhighlight %}

## Arguments

| Argument       | Description                                                                                             | Type     | Required |
| :------------- | :------------------------------------------------------------------------------------------------------ | :------- | -------- |
| `<route-path>` | path for the route to be created (ex : example/my-route). If not provided it will be asked to the user. | `string` | `false`  |

## Options

| Option         | Description                 |
| :------------- | :-------------------------- |
| `--no-service` | skip the service generation |

## Example

{% highlight bash %}
$ sk route:create
{% endhighlight %}
