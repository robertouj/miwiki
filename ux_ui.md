---
title: UX-UI
description: 
published: true
date: 2022-04-02T21:55:22.231Z
tags: 
editor: markdown
dateCreated: 2022-04-02T21:55:20.976Z
---

# UX-UI

## Add Google Fonts to a website

Goes to [Google Fonts website](https://fonts.google.com/), select a font and:

Copy the code of head tag:

```html
<head>
  <!-- Other head tags -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Palette+Mosaic&family=Roboto:wght@100&display=swap" rel="stylesheet">
  <!-- Other head tags -->
</head>
```

Copy the code for the css rules:

```css
font-family: 'Palette Mosaic', cursive;
font-family: 'Roboto', sans-serif;
```

## Add css loading spinner

From the website <https://loading.io/css>. Copy the css and the html and add it to the code.

## API with Mock data

Free fake API for testing and prototyping.

https://jsonplaceholder.typicode.com/

## Fake JSON API

https://github.com/typicode/json-server

## Writing formated text in HTML5

The `<pre>` HTML element represents preformatted text which is to be presented exactly as written in the HTML file.

For example with JSX:

```jsx
<pre>
{
  "x": 28,
  "y": 97
}
</pre>
```

It shows:

```html
{
  "x": 28,
  "y": 97
}
```
