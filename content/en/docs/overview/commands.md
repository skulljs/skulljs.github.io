---
title: "Commands"
description: "Skulljs comes with a CLI and commands for performing common tasks."
lead: "Skulljs comes with a CLI and commands for performing common tasks."
date: 2023-04-19T14:46:29+02:00
lastmod: 2023-04-19T14:46:29+02:00
draft: false
images: []
menu:
  docs:
    parent: "overview"
weight: 130
toc: true
---

---

## sk new

Create new project based on github repositories templates

### Usage

```bash
sk new <project-name> [options]
sk n <project-name> [options]
```

### Arguments

| Argument         | Description             | Type     | Required |
| :--------------- | :---------------------- | :------- | -------- |
| `<project-name>` | name of the new project | `string` | `true`   |

### Options

| Option         | Description                     |
| :------------- | :------------------------------ |
| `--back` `-b`  | generate only the backend part  |
| `--front` `-f` | generate only the frontend part |

### Example

```bash
sk new my-awesome-project
```

---

## sk route:create

### Feature

Create a new route for the backend repository and a new service for the frontend repository based on the user's answers

### Usage

```bash
sk route:create <route-path> [options]
sk rc <route-path> [options]
```

### Arguments

| Argument       | Description                                                                                             | Type     | Required |
| :------------- | :------------------------------------------------------------------------------------------------------ | :------- | -------- |
| `<route-path>` | path for the route to be created (ex : example/my-route). If not provided it will be asked to the user. | `string` | `false`  |

### Options

| Option         | Description                 |
| :------------- | :-------------------------- |
| `--no-service` | skip the service generation |

### Example

```bash
sk route:create
```

---

## sk doc

### Feature

Generate the documentation for the skulljs project

### Usage

```bash
sk doc
```

### Example

```bash
sk doc
```

---

## sk build

### Feature

Build both frontend and backend projects into a dist folder ready to be used for PM2 or Docker.

See [deployment guide](/docs/deployment) for more informations.

### Usage

```bash
sk build
```

### Example

```bash
sk build
```
