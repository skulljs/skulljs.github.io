---
title: "Create a REST API route from database"
description: "One page summary of how to create a REST API route from database in a Skulljs project."
lead: "One page summary of how to create a REST API route from database in a Skulljs project."
date: 2023-04-21T09:34:29+02:00
lastmod: 2023-04-21T09:34:29+02:00
draft: false
images: []
menu:
  docs:
    parent: "how-to"
weight: 210
toc: true
---

## Requirements

- Working project — check that your project works locally
- ORM's schema file filled - ensure the descriptions of the database tables are correct
- [Node.js](https://nodejs.org/) — latest LTS version or newer
- [Skulljs-cli](https://www.npmjs.com/package/@skulljs/cli) — the version which you created the project or newer

{{< details "Why ORM's schema file?" >}}
Skulljs parse the ORM's schema file to retrieve database description and generate the REST API route on top of the model you select.
{{< /details >}}

## Create a REST API route from database

Use the Skulljs CLI to generate files.

### Use sk route:create

```bash
sk route:create
```

1. Enter the path of the route
{{< alert icon="👉" >}}
The generated files are automatically placed in the routes folder of the backend
{{< /alert >}}
1. Select a database model
1. Select which CRUD's parts you want to generate
1. Tell the CLI if you want the frontend service files to be generated aswell

That's all you files are now generated and ready to be used.
