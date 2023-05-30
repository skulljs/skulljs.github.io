---
title: "NestJs Features"
description: "We have implemented configurable features to make using the NestJs component of Skulljs as easy as possible."
lead: "We have implemented configurable features to make using the NestJs component of Skulljs as easy as possible."
date: 2023-04-21T10:54:29+02:00
lastmod: 2023-04-21T10:54:29+02:00
draft: false
images: []
menu:
  docs:
    how-to:
      parent: "features"
weight: 222
toc: true
---

## NestJs Documentation

For more information check out the official documentation.

[Official NestJs Documentation →](https://docs.nestjs.com/)

## Global Configuration

The configuration for the global features can be found in the file detailed below.

{{< alert icon="👉" >}}
Enabling or disabling these configurations would impact the entire NestJs component.
{{< /alert >}}

```typescript
// backend/src/configs/configuration.ts
export const configuration = () => ({
  // Api

  production: false,
  // general prefix for nestjs routes
  apiPrefix: "api",
  // nestjs port
  port: 3000,

  // Access Logger

  // the max size of the file before it rotates
  accessLoggerFileSize: "10M",
  // the max time before it rotates
  accessLoggerFileInterval: "1d",

  // Helmet

  // false for sk build
  helmetContentSecurityPolicy: false,

  // Cors

  // allowed origins | Ex: angular
  corsOrigins: ["http://localhost:4200"],

  // OpenApi

  // path of the open api docs
  openAPIPath: "api",
  // title of the open api docs
  openAPITitle: "skulljs nestjs example",
  // description of the open api docs
  openAPIDescription: "nestjs component for skulljs",
  // version of the open api docs
  openAPIVersion: "1.0",

  // Session

  // ! you need to change this
  sessionSecret: "changeMeOrInsecure",
  // value in ms | 1 day
  sessionCookieMaxAge: 86400000,
  // true = Forces the session to be saved back to the session store, even if the session was never modified during the request.
  sessionResave: false,
  // true = Forces a session that is "uninitialized" to be saved to the store. A session is uninitialized when it is new but not modified.
  sessionSaveUninitialized: false,
  // Specifies the boolean value for the HttpOnly Set-Cookie attribute.
  sessionCookieHttpOnly: false,
  // Specifies the boolean value for the Secure Set-Cookie attribute.
  sessionCookieSecure: "auto",

  // Mailer

  // Smtp Host
  mailerSmtpHost: "smtp.example.com",
  // Smtp Port
  mailerSmtpPort: 25,
  // Default from for mails
  mailerDefaultFrom: '"skulljs" <skulljs@example.com>',
  // Email address for mail diversion in dev env
  mailerDevEnvRedirectEmail: 'redirect@example.com', 

  // Crypto

  // ! you need to change this, === 32 characters
  cryptoSecretKey: "changeMeOrInsecure".padEnd(32, "!"),
  // ! you need to change this
  cryptoHashSaltString: 'changeMeOrInsecure', 
});
```

## ORM: Prisma

We have selected Prisma as the ORM for the NestJs component of Skulljs.

{{< details "Why Prisma?" >}}

1. **Easy to Use**: Prisma is designed to be easy to use. Its declarative syntax makes it easy to read and understand the code, even for developers who are not familiar with the underlying database technology.
1. **Performance**: Prisma is optimized for performance, with features like query batching and automatic query optimization that can significantly reduce the number of database requests and improve response times. Prisma also uses modern database connectors like PostgreSQL and MySQL to ensure that data is retrieved and processed as quickly as possible.
1. **Flexibility**: Prisma is highly flexible and can be used with a wide range of databases and technologies. It supports multiple databases, including MySQL, PostgreSQL, and SQLite.
1. **Strong Type Safety**: Prisma provides strong type safety by generating TypeScript types for your database schema. This helps to catch errors early and ensures that your code is more robust and reliable.
1. **Open-Source**: Prisma is an open-source project that is actively maintained by a community of developers. This means that it is free to use and can be customized and extended to meet your specific needs.
   {{< /details >}}

For more information check out the official documentation.

[Official Prisma Documentation →](https://www.prisma.io/docs)

### Schema

The database schema can be found in the file detailed below.

{{< alert icon="👉" >}}
The database config is located in _backend/.env_
{{< /alert >}}

```typescript
// backend/prisma/schema.prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
}

model Cats {
  id         Int    @id @default(autoincrement())
  name       String
  color      String
  weight     String
  eyes_color String
}
```

### Seeder

The seeder can be found in the file detailed below.

{{< alert icon="👉" >}}
You can use [faker](https://fakerjs.dev/) to generate fake data.
{{< /alert >}}

```typescript
// backend/prisma/seed.ts
import { faker } from '@faker-js/faker';
import { PrismaClient, Cats } from '@prisma/client';
const prisma = new PrismaClient();

async function main() {
  const data: Cats[] = [];
  for (let i = 1; i <= 50; i++) {
    data.push({ id: i, name: faker.animal.cat(), color: faker.color.human(), weight: faker.number.int().toString(), eyes_color: faker.color.human() });
  }

  const cats = await prisma.cats.createMany({ data, skipDuplicates: true });
  console.log({ cats });
}

main().catch(async (err) => {
  console.log(err);
  await prisma.$disconnect();
  process.exit(1);
});
```

### Usage

We have created a service to facilitate NestJs integration. Here are the instructions on how to use it.

```typescript
// any route module
import { PrismaService } from "src/prisma.service";

@Module({
  controllers: [CatsController],
  providers: [CatsService, PrismaService],
})
export class CatsModule {}
```

```typescript
// any route service
import { PrismaService } from "src/prisma.service";

@Injectable()
export class CatsService {
  constructor(private readonly prisma: PrismaService) {}

  findAll() {
    return this.prisma.cats.findMany();
  }
}
```

## Session

Skulljs's NestJs component comes with a built-in session manager.

### Session settings

The session's settings can be found in the file detailed below.

{{< alert icon="⚠️" >}}
You need to change the session secret.
{{< /alert >}}

```typescript
// backend/src/configs/configuration.ts
export const configuration = () => ({
  // Session

  // ! you need to change this
  sessionSecret: "changeMeOrInsecure",
  // value in ms | 1 day
  sessionCookieMaxAge: 86400000,
  // true = Forces the session to be saved back to the session store, even if the session was never modified during the request.
  sessionResave: false,
  // true = Forces a session that is "uninitialized" to be saved to the store. A session is uninitialized when it is new but not modified.
  sessionSaveUninitialized: false,
  // Specifies the boolean value for the HttpOnly Set-Cookie attribute.
  sessionCookieHttpOnly: false,
  // Specifies the boolean value for the Secure Set-Cookie attribute.
  sessionCookieSecure: "auto",
});
```

### Session type

The description of the session type can be found in the file detailed below.

```typescript
// backend/src/types/session.d.ts
import "express-session";

declare module 'express-session' {
  interface Session {
    user?: {
      isLogged: boolean;
      role?: Roles;

      // Declare here your session data
    };
  }
}
```

### Usage

```typescript
// any route controller or service
import { ..., Session } from '@nestjs/common';
import { Session as SessionExpress } from 'express-session';

@Controller('cats')
export class CatsController {
  ...
  @Get('admin')
  admin(@Session() session: SessionExpress) {
    return this.catsService.admin(session);
  }
}
```

## IsAuthorized Guard

To simplify access management of NestJs routes, Skulljs comes equipped with a built-in guard named `IsAuthorized`.

The guard comes with two modes:

- **Minimun Role Mode**: check if the user have the listed role or a superior one
- **List Role Mode**: check if the user have one of the listed roles

You can switch the mode with the _minimunRoleMode_ boolean.

### Roles description

You can add or remove any roles in the file detailed below.

```typescript
// backend/src/guards/is-authorized/roles.ts
export enum Roles {
  LoggedUser = 10,
  Admin = 80,
  // Example
  MyRole = 20,
}
```

### Usage

```typescript
// any route controller
import { Authorize } from 'src/decorators/authorize.decorator';
import { Roles } from 'src/guards/is-authorized/roles';

@Controller('cats')
export class CatsController {
  ...
  @Get('admin')
  @Authorize([Roles.MyRole], {minimunRoleMode: true})
  admin() {
    return this.catsService.admin();
  }
}
```

## Mailer

Skulljs's NestJs component comes with a build-in mailer.

The mailer redirect all mail to the mailerDevEnvRedirectEmail defined in config while the app is in dev env.

### Mailer settings

The mailer settings can be found in the file detailed below.

```typescript
// backend/src/configs/configuration.ts
export const configuration = () => ({
  // Mailer

  // Smtp Host
  mailerSmtpHost: "smtp.example.com",
  // Smtp Port
  mailerSmtpPort: 25,
  // Default from for mails
  mailerDefaultFrom: '"skulljs" <skulljs@example.com>',
  // Email address for mail diversion in dev env
  mailerDevEnvRedirectEmail: 'redirect@example.com', 
});
```

### Mailer usage

```typescript
// any route service
import { MailerService } from '@nestjs-modules/mailer';
import * as Utils from '../../utils/utils';

@Injectable()
export class CatsService {
  constructor(private readonly mailerService: MailerService, ...) {}
  ...
  sendMail() {
    Utils.sendMail(this.mailerService, {
      to: 'user.name@example.com', // list of receivers
      subject: '[skulljs] The cats have been created ✔', // Subject line
      template: 'cats',
      context: {
        // Data to be sent to template engine.
        name: 'john doe',
      },
    });
  }
}
```

## Utils

Skulljs's Nestjs component comes with built-in utils.

### Array.prototype.asyncForEach

Asynchronous forEach

{{< alert icon="👉" >}}
No need to import. This util is globally imported in the Nestjs component
{{< /alert >}}

```typescript
const data = [];
const cats = await this.prisma.cats.findMany();
await cats.asyncForEach(async (cat) => {
  const food = await this.prisma.foods.findUnique({ where: { id: cat.food_id } });
  data.push({ cat, food });
});
```

### Array.prototype.shuffle

Function to shuffle an array

{{< alert icon="👉" >}}
No need to import. This util is globally imported in the Nestjs component
{{< /alert >}}

```typescript
const cats = await this.prisma.cats.findMany();
const cats_shuffle = cats.shuffle();
```

### TemplateToPDF

PDF generation from Handlebars template

{{< alert icon="👉" >}}
You can add templates in backend/templates/pdfs/
{{< /alert >}}

```typescript
// any route service
import * as Utils from '../../utils/utils';

@Injectable()
export class CatsService {
  ...
  async printPDFFromTemplate(id: number): Promise<Buffer> {
    const cat = await this.prisma.cats.findUnique({ where: { id } });
    return Utils.templateToPDF({ template: 'cats', context: { cat } });
  }
}
```

### PDFGenerator

PDF generation from class

{{< alert icon="👉" >}}
You can add functions in backend/src/utils/classes/PDFGenerator.ts
{{< /alert >}}

```typescript
// any route service
import * as Utils from '../../utils/utils';

@Injectable()
export class CatsService {
  ...
  async printPDFFromClass(id: number): Promise<Buffer> {
    const cat = await this.prisma.cats.findUnique({ where: { id } });
    const pdf = new Utils.PDFGenerator()
      .createDocument()
      .addNewPageListener()
      .newPage()
      .writeTitle('Export Cat')
      .writeSubtitle(`Cat N°${cat.id}`)
      .writeLabelValuePair('name', cat.name, 200)
      .writeLabelValuePair('weight', cat.weight, 200)
      .writeLabelValuePair('color', cat.color, 200)
      .writeLabelValuePair('eyes_color', cat.eyes_color, 200);

    return pdf.closeAndGetBytes();
  }
}
```

### Encrypt, Decrypt and Hash

Functions for encrypt, decrypt and hash

{{< alert icon="⚠️" >}}
You need to change the configuration found in backend/src/configs/configuration.ts
{{< /alert >}}

```typescript
// any route service
import * as Utils from '../../utils/utils';

@Injectable()
export class CatsService {
  ...
  async crypto() {
    const rawData = 'iAmATestString';
    const encryptedData = Utils.crypto.encrypt(rawData);
    return { rawData: Utils.crypto.decrypt(encryptedData), encryptedData: encryptedData, hash: await Utils.crypto.hash(rawData) };
  }
}
```

## Open API

For the API documentation Skulljs uses [Open API](https://www.openapis.org/). The default URL for Open API documentation is [http://localhost:3000/api](http://localhost:3000/api).

### Open API settings

The Open API settings can be found in the file detailed below.

```typescript
// backend/src/configs/configuration.ts
export const configuration = () => ({
  // OpenAPI

  // path of the open api docs
  openAPIPath: "api",
  // title of the open api docs
  openAPITitle: "skulljs nestjs example",
  // description of the open api docs
  openAPIDescription: "nestjs component for skulljs",
  // version of the open api docs
  openAPIVersion: "1.0",
});
```

### Usage

{{< alert icon="👉" >}}
The Open API models are automatically generated from entities and DTOs
{{< /alert >}}

```typescript
// any route controller
import { ApiTags, ApiOkResponse } from '@nestjs/swagger';
import { Cat } from './entities/cat.entity';

@ApiTags('cats')
@Controller('cats')
export class CatsController {
  ...
  @Get()
  @ApiOkResponse({ type: Cat })
  findAll() {
    return this.catsService.findAll();
  }
}
```
