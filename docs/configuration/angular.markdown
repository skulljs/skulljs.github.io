---
layout: default
title: Angular
description: Configuration of the angular template.
parent: Configuration
last_modified_date: 2022-11-18 10:53
---

# Configuration of angular
{: .no_toc }
To make it as easy as possible to use angular, we made configurable features. Check below for details
{: .fs-6 .fw-300 }

The list of those features is available [here](/docs/features/angular)

---

## Table of contents
{: .no_toc  .text-delta}

- TOC
{:toc}

---

## Loader directive

The configuration of the loader directive is located at **frontend/src/app/modules/directives/loader.directive.ts**.

{% highlight ts %}
@Input() loaderSource = 'assets/images/loader.gif';
@Input() loaderHeight = '200px';
@Input() loaderWidth = '200px';
{% endhighlight %}

## Skulljs style

The configuration of the style is located at **frontend/src/assets/scss/_layout.scss** and **frontend/src/assets/scss/_variables.scss**.

The configuration can be activate / desactivate at **frontend/src/styles.scss**.

We recommend using material on top of this.
