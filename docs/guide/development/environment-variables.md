# Environment Variables

Sneat comes with support for environment variables, which allows you to use `.env` to load the environment variables.

:::warning Tip
We recommend you to read the [official guide](https://nextjs.org/docs/basic-features/environment-variables) given by Next.js for using environment variables.
:::

## Loading Environment Variables

Next.js has built-in support for loading environment variables from `.env` file into `process.env`.

An example `.env.local`:

```bash
DB_HOST=localhost
DB_USER=myuser
DB_PASS=mypassword
```

This loads `process.env.DB_HOST`, `process.env.DB_USER`, and `process.env.DB_PASS` into the Node.js environment automatically allowing you to use them in [Next.js data fetching methods](https://nextjs.org/docs/basic-features/data-fetching/overview) and [API routes](https://nextjs.org/docs/api-routes/introduction).

For example, using [getStaticProps](https://nextjs.org/docs/basic-features/data-fetching/get-static-props):

```tsx
// pages/index.js
export async function getStaticProps() {
  const db = await myDB.connect({
    host: process.env.DB_HOST,
    username: process.env.DB_USER,
    password: process.env.DB_PASS
  })
  // ...
}
```

## Exposing Environment Variables to the Browser

By default environment variables are only available in the Node.js environment, meaning they won't be exposed to the browser.

In order to use an environment variable inside a component and to expose a variable to the browser, you have to prefix the variable with `NEXT_PUBLIC_`. For example:

```bash
NEXT_PUBLIC_ANALYTICS_ID=abcdefghijk
```

::: warning
Do not store any secrets (such as private API keys or passwords) in the public variables! These environment variables are embedded into the build, meaning anyone can view them by inspecting your app's files.
:::

## Private Variables

Having access to the `NODE_ENV` is also useful for performing actions conditionally:

```tsx
if (process.env.NODE_ENV !== 'production') {
  analytics.disable()
}
```

Read more nextjs official documentation for more info on environment variables from [here](https://nextjs.org/docs/basic-features/environment-variables).

## Environment variables used in the template

We have use the `fake-db` and fake-db API calls are not supported to access the environment variables. Hence, we have used `NEXT_PUBLIC` prefix with our environment variables. You can find the environment variables' file `.env.development` in the root of the project. The environment variables that we have used in the `.env.development` file are as follows:

```bash
NEXT_PUBLIC_JWT_EXPIRATION
NEXT_PUBLIC_JWT_SECRET
NEXT_PUBLIC_JWT_REFRESH_TOKEN_SECRET
```

Make sure to replace JWT secrets and token with your actual values and it's advisable to remove the `NEXT_PUBLIC` prefix if you are using the Next.js data fetching method or API routes.
