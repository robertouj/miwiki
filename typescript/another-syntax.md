---
title: Another TypeScript syntax
description: 
published: true
date: 2022-05-03T17:59:08.673Z
tags: 
editor: markdown
dateCreated: 2022-05-03T17:55:14.287Z
---

# Another TypeScript syntax

## Non-null Assertion Operator (Postfix !)

TypeScript also has a special syntax for removing `null` and `undefined` from a type without doing any explicit checking. Writing `!` after any expression is effectively a type assertion that the value isn’t `null` or `undefined`:

```TypeScript
function liveDangerously(x?: number | null) {
  // No error
  console.log(x!.toFixed());
}
```

[more info](<https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#non-null-assertion-operator-postfix->)
