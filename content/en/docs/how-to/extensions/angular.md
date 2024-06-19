---
title: "Angular Extensions"
description: "Use our Angular librairies to extends the Angular component features."
lead: "Use our Angular librairies to extends the Angular component features."
date: 2023-04-21T15:22:29+02:00
lastmod: 2024-03-27T10:22:29+02:00
draft: false
images: []
menu:
  docs:
    how-to:
      parent: "extensions"
weight: 231
toc: true
---

## sk loader

Loader for promises.

### Installation

{{< alert icon="👉" >}}
In frontend
{{< /alert >}}

Choose the version matching your angular project.

```bash
npm i @skulljs/angular-loader
```

### Usage

Add it to the import list of your component.

```typescript
// any component
import { SkLoaderModule } from '@skulljs/angular-loader';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [..., SkLoaderModule],
  templateUrl: './app.component.html',
  styleUrl: './app.component.scss',
})
export class AppComponent {}
```

Use it !

{{< alert icon="👉" >}}
The loader is displayed when the boolean is equal to true.
{{< /alert >}}

```html
<div
  [skLoader]="myBoolean"
  loaderHeight="50px"
  loaderWidth="50px"
  loaderSource="https://raw.githubusercontent.com/skulljs/angular-libraries/main/assets/skLoader.gif"
>
  Displayed when loading finished.
</div>
```

## sk scroll to top btn

Smooth scroll to top button.

### Installation

{{< alert icon="👉" >}}
In frontend
{{< /alert >}}

Choose the version matching your angular project.

```bash
npm i @skulljs/angular-scroll-to-top-btn
```

### Usage

Add it to the import list of your component.

```typescript
// any component
import { SkScrollToTopBtnModule } from '@skulljs/angular-scroll-to-top-btn';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [..., SkScrollToTopBtnModule],
  templateUrl: './app.component.html',
  styleUrl: './app.component.scss',
})
export class AppComponent {}
```

Use it !

{{< alert icon="👉" >}}
The arrow color is automatically computed based on the background color.
{{< /alert >}}

```html
<sk-scroll-to-top-btn 
  normalBgColor="#357a9b" 
  hoverBgColor="#004e6d"
  [minDisplayWidth]="500"
  [maxDisplayWidth]="2200"
>
</sk-scroll-to-top-btn>
```
