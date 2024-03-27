---
title: "Angular Features"
description: "We have implemented configurable features to make using the Angular component of Skulljs as easy as possible."
lead: "We have implemented configurable features to make using the Angular component of Skulljs as easy as possible."
date: 2023-04-21T10:04:29+02:00
lastmod: 2023-04-21T10:04:29+02:00
draft: false
images: []
menu:
  docs:
    how-to:
      parent: "features"
weight: 221
toc: true
---

## Angular Documentation

For more information check the official documentation.

[Official Angular Documentation →](https://angular.io/docs)

## Skulljs style

Skulljs's Angular component comes with a built-in starter style. Feel free to edit or remove it.

{{< alert icon="👉" >}}
We recommend using angular material on top of this.
{{< /alert >}}

### Edit the style

```bash
# variables
frontend/src/assets/scss/_variables.scss

# layout
frontend/src/assets/scss/_layout.scss
```

### Disable the style

Comment the following line.

```scss
// frontend/src/style.scss
@import "./assets/scss/layout";
```

## IsAuthorized Guard

To simplify access management of Angular routes, Skulljs comes equipped with a built-in guard named `IsAuthorized`.

The guard comes with two modes:

- **Minimun Role Mode**: check if the user have the listed role or a superior one
- **List Role Mode**: check if the user have one of the listed roles

You can switch the mode with the *minimunRoleMode* boolean.

### Roles description

You can add or remove any roles in the file detailed below.

```typescript
// frontend/src/app/guards/isAuthorized/roles.ts
export enum Roles {
  NonLoggedUser = 0,
  LoggedUser = 10,
  Admin = 80,
  // example
  MyRole = 20,
}
```

### Usage

```typescript
// any routing module
import { isAuthorizedGuard } from "./guards/IsAuthorized/is-authorized.guard";
import { Roles } from "./guards/IsAuthorized/roles";

const routes: Routes = [
  {
    path: 'admin',
    component: AdminComponent,
    canActivate: [isAuthorizedGuard],
    data: {
      authorize: [Roles.Admin],
      minimunRoleMode: true,
      // Redirection url if the user isn't allowed to access the route
      fallbackRoute: '/auth',
    },
  },
];
```
