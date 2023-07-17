---
sidebarDepth: 0
---

# :first-child console error

When we use one of the pseudo-classes  `:first-child`, `:nth-child(N)` or `:nth-last-child(N)`, we may get errors in the browser console like the following:

```text
The pseudo class ":first-child" is potentially unsafe when doing server-side rendering.
The pseudo class ":nth-child(N)" is potentially unsafe when doing server-side rendering.
The pseudo class ":nth-last-child(N)" is potentially unsafe when doing server-side rendering.
```

There is nothing wrong with using these pseudo-classes. This issue is a warning for those who are using server-side rendering that these pseudo-classes might not work.

This issue is not from our template or MUI framework but rather it is from [emotion's](https://emotion.sh/) side. Please read [this issue](https://github.com/emotion-js/emotion/issues/1178) for further details.
