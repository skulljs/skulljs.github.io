---
layout: default
title: NestJs
description: Configuration of the nestjs template.
parent: Configuration
last_modified_date: 2022-11-28 15:52
---

# Configuration of nestjs
{: .no_toc }
To make it as easy as possible to use nestjs, we made configurable features. Check below for details
{: .fs-6 .fw-300 }

The list of those features is available [here](/docs/features/nestjs)

---

## Table of contents
{: .no_toc  .text-delta}

- TOC
{:toc}

---

## Global configuration

The global configuration is located at **backend/src/configs/configuration.ts**.

Activate or deactivate those configuration would affect the whole NestJs template.

{% highlight ts %}
export const configuration = () => ({
  // Api
  apiPrefix: 'api', // general prefix for nestjs routes
  port: 3000, // nestjs port

  // Access Logger
  accessLoggerFileSize: '10M', // the max size of the file before it rotates
  accessLoggerFileInterval: '1d', // the max time before it rotates

  // Helmet
  helmetContentSecurityPolicy: false, // false for sk build

  // Cors
  corsOrigins: ['http://localhost:4200'], // allowed origins | Ex: angular

  // OpenAPI
  openAPIPath: 'api', // path of the open api docs
  openAPITitle: 'skulljs nestjs example', // title of the open api docs
  openAPIDescription: 'nestjs component for skulljs', // description of the open api docs
  openAPIVersion: '1.0', // version of the open api docs

  // Session
  sessionSecret: 'changeMeOrInsecure', // ! you need to change this
  sessionCookieMaxAge: 86400000, // value in ms | 1 day
  sessionResave: false, // true = Forces the session to be saved back to the session store, even if the session was never modified during the request.
  sessionSaveUninitialized: false, // true = Forces a session that is "uninitialized" to be saved to the store. A session is uninitialized when it is new but not modified.
  sessionCookieHttpOnly: false, // Specifies the boolean value for the HttpOnly Set-Cookie attribute.
  sessionCookieSecure: 'auto', // Specifies the boolean value for the Secure Set-Cookie attribute.

  // Mailer
  mailerSmtpHost: 'smtp.example.com', // Smtp Host
  mailerSmtpPort: 25, // Smtp Port
  mailerDefaultFrom: '"skulljs" <skulljs@example.com>', // Default from for mails

  // Crypto
  cryptoSecretKey: 'changeMeOrInsecure'.padEnd(32, '!'), // ! you need to change this, === 32 characters
});
{% endhighlight %}

## IsAuthorized Guard

In other to use our IsAuthorized Guard, you have to put the following lines in your route controller

{% highlight ts %}
@ApiTags('cats')
@Controller('cats')
@UseGuards(IsAuthorizedGuard)
export class CatsController {
  ...
}
{% endhighlight %}

Then, you can use the authorize decorator in your controller to specify for each endpoint the authorized roles

{% highlight ts %}
@Delete(':id')
@Authorize(Roles.Admin)
@ApiOkResponse({ type: Cat })
remove(@Param('id') id: string) {
  return this.catsService.remove(+id);
}
{% endhighlight %}

You can manage the roles and the guard's logic at **backend/src/guards/is-authorized**.
