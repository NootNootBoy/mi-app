# How to remove Fake DB and use Real API

Sneat uses [axios-mock-adapter](https://github.com/ctimmerm/axios-mock-adapter) for mocking API calls. This makes our template **API ready** 😍 and more easier for you to communicate with your backend.

However, you won't need fake-db if you are using real APIs. In this case please follow below steps to remove fake-db from template.

1. Remove `@fake-db` folder from `src` directory
2. Remove fake-db import from `src/pages/_app.tsx` file

```diff
// File: src/pages/_app.tsx

-  // ** Fake-DB Import
-  import 'src/@fake-db'
```

3. Finally we don't need axios-mock-adapter in our package any more so remove it from the `package.json` file

```diff
{
  dependencies: {
-    "axios-mock-adapter": "...",
  }
}
```

This will remove fake-db completely from your package. 🎉

::: warning NOTE
Now all (fake) API calls will result in 404 error until you replace them with your real API endpoints.
:::
