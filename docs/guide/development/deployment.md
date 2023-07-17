# Deployment

::: tip

Read [official Next.js docs](https://nextjs.org/docs/deployment) to handle deployment smoothly.
:::
## Node.js Server

Next.js can be deployed to any hosting provider that supports Node.js. Make sure your `package.json` has the `build` and `start` scripts:

```json
"scripts": {
  "dev": "next dev",
  "build": "next build",
  "start": "next start"
}
```

`next build` builds the production application in the `.next` folder. After building, `next start` starts a Node.js server that supports hybrid pages, serving both statically generated and server-side rendered pages.

## Static HTML Export

Command `next export` allows you to export your app to static HTML, which can be run standalone without the need of a Node.js server.

The exported app supports almost every feature of Next.js, including dynamic routes, prefetching, preloading and dynamic imports.

`next export` works by pre-rendering all pages to HTML. For dynamic routes, your page can export a `getStaticPaths` function to let the exporter know which HTML pages to generate for that route.

By default, `next export` will generate an `out` directory, which can be served by any static hosting service or CDN.

The choice of your server software isn’t important either. Since the output of the export command is completely platform-agnostic, there’s no need to explicitly use Node.

::: warning
We are using `img` element instead of [nextjs/Image](https://nextjs.org/docs/api-reference/next/image). If you're using `nextjs/Image` instead of `img` element then you'll get image optimization error with static HTML export. You'll need a loader to fix this. Read this [doc](https://nextjs.org/docs/api-reference/next/image#loader-configuration) for more info.
:::

## Vercel Deployment

Read the this [documentation](https://nextjs.org/docs/deployment#managed-nextjs-with-vercel) to deploy your app to vercel.

::: danger Heads Up!
If you are going to deploy your project under a subfolder, please read this [FAQ](/faq/why-images-are-missing-on-deployment.html) before generating build or exporting your project.
:::
