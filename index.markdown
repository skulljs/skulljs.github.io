---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Home
description: Skulljs is a open source project for building web applications based on Javascript / Typescript. Join the project now !
last_modified_date: 2022-11-16 16:10
nav_order: 1
---

# Focus on the code not the structure

Skulljs aims to give a solid structure to create web applications based on Javascript / Typescript with popular frameworks.
{: .fs-6 .fw-300 }

[Get started now](/docs/getting_started){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [View it on GitHub](https://github.com/skulljs){: .btn .fs-5 .mb-4 .mb-md-0 }

---

Here is some features built in Skulljs:

## Skulljs CLI

- The [skulljs-cli](https://www.npmjs.com/package/@skulljs/cli), several commands and utilities
- `sk new <project_name>`: create a project with frontend and backend to choose in a list
- `sk route:create`: generation of backend routes and frontend services from a database table for CRUD
- `sk build`: create a dist folder ready to deploy for PM2 or Docker
- more commands availables [here](/docs/cli-and-commands)

## NestJs

- Prisma
- Optional use of Faker to populate the database with fake data
- PDF generation from a customizable class named PDFGenerator
- PDF generation from EJS templates
- Email generation from EJS templates
- A built-in logger using Morgan
- A built-in middleware for check if a user is logged
- A built-in security middleware using Helmet
- Cors support
- Session support using express-session
- Integration of Compodoc and OpenAPI

## Angular

- An Angular directive to handle pre-loaders
- Integration of Compodoc

---

## About the project

Skulljs is &copy; 2021-{{ "now" | date: "%Y" }}

### License

Skulljs is distributed by an [MIT license](https://choosealicense.com/licenses/mit/).
