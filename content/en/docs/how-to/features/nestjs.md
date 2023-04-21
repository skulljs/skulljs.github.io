---
title: "NestJs Features"
description: "To make it as easy as possible to use NestJs component of Skulljs, we made configurable features."
lead: "To make it as easy as possible to use NestJs component of Skulljs, we made configurable features."
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

For more information check the official documentation.

[Official NestJs Documentation →](https://docs.nestjs.com/)

## Global Configuration

The global feature's configuration is located at the file detailled below.

{{< alert icon="👉" >}}
Activate or deactivate those configurations would affect the whole NestJs component.
{{< /alert >}}

```typescript
// backend/src/configs/configuration.ts
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
```

## ORM: Prisma

We choose Prisma as the ORM of the NestJs component of Skulljs.

{{< details "Why Prisma?" >}}

1. __Easy to Use__: Prisma is designed to be easy to use. Its declarative syntax makes it easy to read and understand the code, even for developers who are not familiar with the underlying database technology.
1. __Performance__: Prisma is optimized for performance, with features like query batching and automatic query optimization that can significantly reduce the number of database requests and improve response times. Prisma also uses modern database connectors like PostgreSQL and MySQL to ensure that data is retrieved and processed as quickly as possible.
1. __Flexibility__: Prisma is highly flexible and can be used with a wide range of databases and technologies. It supports multiple databases, including MySQL, PostgreSQL, and SQLite.
1. __Strong Type Safety__: Prisma provides strong type safety by generating TypeScript types for your database schema. This helps to catch errors early and ensures that your code is more robust and reliable.
1. __Open-Source__: Prisma is an open-source project that is actively maintained by a community of developers. This means that it is free to use and can be customized and extended to meet your specific needs.
{{< /details >}}

For more information check the official documentation.

[Official Prisma Documentation →](https://www.prisma.io/docs)

### Schema

The database schema is located at the file detailled below.

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

The seeder is located at the file detailled below.

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
    data.push({ id: i, name: faker.animal.cat(), color: faker.color.human(), weight: faker.random.numeric(), eyes_color: faker.color.human() });
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

We made a service for easier NestJs integration. Here is how to use it.

```typescript
// any route module
import { PrismaService } from 'src/prisma.service';

@Module({
  controllers: [CatsController],
  providers: [CatsService, PrismaService],
})
export class CatsModule {}
```

```typescript
// any route service
import { PrismaService } from 'src/prisma.service';

@Injectable()
export class CatsService {
  constructor(private readonly prisma: PrismaService) {}

  findAll() {
    return this.prisma.cats.findMany();
  }
}
```

## Session

Skulljs's NestJs component comes with built-in session manager.

### Session settings

The session settings are located at the file detailled below.

{{< alert icon="🛑" >}}
You need to change the session secret.
{{< /alert >}}

```typescript
// backend/src/configs/configuration.ts
export const configuration = () => ({
  // Session
  sessionSecret: 'changeMeOrInsecure', // ! you need to change this
  sessionCookieMaxAge: 86400000, // value in ms | 1 day
  sessionResave: false, // true = Forces the session to be saved back to the session store, even if the session was never modified during the request.
  sessionSaveUninitialized: false, // true = Forces a session that is "uninitialized" to be saved to the store. A session is uninitialized when it is new but not modified.
  sessionCookieHttpOnly: false, // Specifies the boolean value for the HttpOnly Set-Cookie attribute.
  sessionCookieSecure: 'auto', // Specifies the boolean value for the Secure Set-Cookie attribute.
});
```

### Session type

The description of the session type is located at the file detailled below.

```typescript
// backend/src/types/session.d.ts 
import 'express-session';

declare module 'express-session' {
  interface Session {
    user?: {
      isLogged: boolean;
      isAdmin?: boolean;
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

In order to facilitate the NestJs's routes access management, Skulljs come with a built-in guard named IsAuthorized.

### Roles description

You can add or remove any roles in the file detailled below.

```typescript
// backend/src/guards/is-authorized/roles.ts 
export enum Roles {
  LoggedUser,
  Admin,
  // Example 
  MyRole
}
```

### Guard logic

You can edit the guard logic in the file detailled below.

```typescript
// backend/src/guards/is-authorized/is-authorized.guard.ts
validateRequest(session: SessionExpress, authorize: Roles[]) {
  ...
  if (session.user && authorize.includes(Roles.MyRole)) {
    isAuthorized = <condition>;
  }
  return isAuthorized;
}
```

### Usage

```typescript
// any route controller
import { ..., UseGuards } from '@nestjs/common';
import { IsAuthorizedGuard } from 'src/guards/is-authorized/is-authorized.guard';
import { Authorize } from 'src/decorators/authorize.decorator';
import { Roles } from 'src/guards/is-authorized/roles';

@Controller('cats')
@UseGuards(IsAuthorizedGuard)
export class CatsController {
  ...
  @Get('admin')
  @Authorize(Roles.MyRole)
  admin() {
    return this.catsService.admin();
  }
}
```


## Mailer

Skulljs's NestJs component comes with build-in mailer.

### Mailer settings

The mailer settings are located at the file detailled below.

```typescript
// backend/src/configs/configuration.ts
export const configuration = () => ({
  // Mailer
  mailerSmtpHost: 'smtp.example.com', // Smtp Host
  mailerSmtpPort: 25, // Smtp Port
  mailerDefaultFrom: '"skulljs" <skulljs@example.com>', // Default from for mails
});
```

### Mailer usage

```typescript
// any route service
import { MailerService } from '@nestjs-modules/mailer';

@Injectable()
export class CatsService {
  constructor(private readonly mailerService: MailerService, ...) {}
  ...
  sendMail() {
    this.mailerService
      .sendMail({
        to: 'user.name@example.com', // list of receivers
        from: 'noreply@skulljs.com', // sender address
        subject: '[skulljs] The cats have been created ✔', // Subject line
        template: 'cats',
        context: {
          // Data to be sent to template engine.
          name: 'john doe',
        },
      })
      .then((success) => {
        console.log(success);
      })
      .catch((err) => {
        console.log(err);
      });
  }
}
```

## Utils

Skulljs's Nestjs component comes with built-in utils.

### Array.prototype.asyncForEach

Asynchronous forEach

{{< alert icon="👉" >}}
No need to import. This util is already imported to all the Nestjs component
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
No need to import. This util is already imported to all the Nestjs component
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

{{< alert icon="🛑" >}}
You need to change the configuration located in backend/src/configs/configuration.ts
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

For the API documentation Skulljs use [Open API](https://www.openapis.org/). The default URL for Open API documentation is  [http://localhost:3000/api](http://localhost:3000/api).

### Open API settings

The Open API settings are located at the file detailled below.

```typescript
// backend/src/configs/configuration.ts
export const configuration = () => ({
  // OpenAPI
  openAPIPath: 'api', // path of the open api docs
  openAPITitle: 'skulljs nestjs example', // title of the open api docs
  openAPIDescription: 'nestjs component for skulljs', // description of the open api docs
  openAPIVersion: '1.0', // version of the open api docs
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
