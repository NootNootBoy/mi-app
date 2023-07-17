---
sidebarDepth: 0
---

# Why Next.js image component doesn't work with next export?

We haven't used the Next.js image component in our template as it doesn't work with the `next export`.

The reason is that the default Next.js loader is not compatible with the Next.js image optimization API. So when we run the `next export` command, it throws an error.

Please refer to [this](https://nextjs.org/docs/messages/export-image-api) docs confirming this issue. It shows the possible ways to solve this issue as well.
