---
title: "Angular Features"
description: "To make it as easy as possible to use Angular component of Skulljs, we made configurable features."
lead: "To make it as easy as possible to use Angular component of Skulljs, we made configurable features."
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

Skulljs's Angular component comes with a built-in starter style. You are free to edit or remove it.

{{< alert icon="👉" >}}
We recommend using material on top of this.
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
@import './assets/scss/layout';
```

## IsAuthorized Guard

In order to facilitate the Angular's routes access management, Skulljs come with a built-in guard named IsAuthorized.

### Roles description

You can add or remove any roles in the file detailled below.

```typescript
// frontend/src/app/guards/isAuthorized/roles.ts
export enum Roles {
  NonLoggedUser,
  LoggedUser,
  Admin,
  // example
  MyRole
}
```

### Guard logic

You can edit the guard logic in the file detailled below.

```typescript
// frontend/src/app/guards/isAuthorized/is-authorized.guard.ts
async function validate(authorize: Roles[]) {
  ...

  if (authorize.includes(Roles.MyRole)) {
    isAuthorized = <condition>;
    isLogged = true;
  }

  return isAuthorized;
}
```

### Usage

```typescript
// any routing module
import { isAuthorizedGuard } from './guards/IsAuthorized/is-authorized.guard';
import { Roles } from './guards/IsAuthorized/roles';

const routes: Routes = [
  { 
    path: 'admin', 
    component: AdminComponent, 
    canActivate: [isAuthorizedGuard], 
    data: { authorize: [Roles.MyRole] }
  }
];
```