---
layout: default
title: sk new
description: Description of the sk new command
parent: CLI and commands
last_modified_date: 2022-11-16 17:01
---

# sk new

## Feature

Create new project based on the repositories template

## Usage

{% highlight bash %}
$ sk new <project-name> [options]
$ sk n <project-name> [options]
{% endhighlight %}

## Arguments

| Argument         | Description             | Type     | Required |
| :--------------- | :---------------------- | :------- | -------- |
| `<project-name>` | name of the new project | `string` | `true`   |

## Options

| Option         | Description                    |
| :------------- | :----------------------------- |
| `--back` `-b`  | generate only the backend part  |
| `--front` `-f` | generate only the frontend part |

## Example

{% highlight bash %}
$ sk new my-awesome-project
{% endhighlight %}
