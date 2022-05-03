---
title: Another TypeScript syntax
description: 
published: true
date: 2022-05-03T17:55:14.287Z
tags: 
editor: markdown
dateCreated: 2022-05-03T17:55:14.287Z
---

# Another TypeScript syntax

## Non-null Assertion Operator (Postfix !)

```TypeScript
function liveDangerously(x?: number | null) {
  // No error
  console.log(x!.toFixed());
}
```