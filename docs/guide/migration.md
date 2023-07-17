---
sidebarDepth: 0
---

# Migration Guide

## 1.0.0 to 1.1.0

The main reason behind this release is to make the template compatible with the latest **Next.js v13**.

- We suggest you to compare your `package.json` file with the template’s `package.json` file first and update all the dependencies according to the template.
- Replace your `src/@core` folder with the template’s `src/@core` folder.
- Due to Next.js v13 update, most of your links may break. Please refer Next.js v13 [guide](https://nextjs.org/docs/advanced-features/codemods#new-link) to fix this change. We have already fixed this in the template but you must manually fix all the links in your project. If you have used Next.js Image component, then you need to manually update your Image components according to [this guide](https://nextjs.org/blog/next-13#nextimage). We have not used Next.js Image component in the template and thus we didn't need to fix them. Please refer to the official Next.js [blog](https://nextjs.org/blog/next-13) for detailed explanation on what has been updated in the Next.js v13.
