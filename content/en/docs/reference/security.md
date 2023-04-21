---
title: "Security"
description: "Skulljs's security measures."
lead: "Skulljs's security measures."
date: 2023-04-21T16:00:29+02:00
lastmod: 2023-04-21T16:00:29+02:00
draft: false
images: []
menu:
  docs:
    parent: "reference"
weight: 310
toc: true
---

## Introduction

Web security is an essential aspect of modern-day computing because the internet is a vast and interconnected network of devices, systems, and services that are constantly exposed to a wide range of security threats, including SQL injection, cross-site scripting (XSS), cross-site request forgery (CSRF), and more.

That's why in Skulljs we have some built-in security measures and best practice.

## Skulljs's Security measures

### Secure Authentication

Secure authentication mechanisms should be implemented to ensure that only authorized users have access to the application. This includes using strong passwords, and encryption. That's why there are built-in guards and crypto functions in Skulljs

### Secure Communication

The Skulljs's deployment method is capable of use HTTPS/SSL/TLS to encrypt communication between the application and the user to prevents attackers from intercepting sensitive information, such as login credentials or payment details. Furthermore, we are using helmet library to add a layout a security in the request headers.

### Input validation

As Skulljs's is build on top of popular frameworks. The popular input attacks are taking in count, this includes checking for SQL injections, cross-site scripting attacks, and other vulnerabilities.

### Session Management

Skulljs comes with a session manager to guarantee proper session management. This ensure that sessions are terminated after a period of inactivity or when a user logs out.

### Access Control

Access control mechanisms should be implemented to ensure that users only have access to the resources they are authorized to access. This includes role-based access control and access control lists. That's why there are built-in guards in Skulljs.

### Logging and Monitoring

Logging and monitoring should be implemented to detect and respond to security incidents. This includes monitoring for unusual activity and analyzing logs for suspicious events. That's why Skulljs comes with a logger for the backend.

### Regular Updates and Patches

All Skulljs's components are getting regular updates and patches thanks to [Depfu](https://depfu.com/) and [Mergify](https://mergify.com/). This ensure that known vulnerabilities are addressed and that the components are up-to-date with the latest security measures.
