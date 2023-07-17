# Loaders

## Pace Loader (Page Loader)

We're using [nprogress](https://github.com/rstacruz/nprogress) as the paceloader (or page loader).

If you want to disable it, change the `routingLoader` property to `false` in the `src/configs/themeConfig.ts` file.

But if you want to remove the package, follow these steps:

- Remove `nprogress` & `@types/nprogress` packages from the `package.json` file
- Remove the following snippet in the `src/pages/_app.ts` file

```tsx
import NProgress from 'nprogress'

// ** Pace Loader
if (themeConfig.routingLoader) {
  Router.events.on('routeChangeStart', () => {
    NProgress.start()
  })
  Router.events.on('routeChangeError', () => {
    NProgress.done()
  })
  Router.events.on('routeChangeComplete', () => {
    NProgress.done()
  })
}
```

## Splash Screen (Loader with Logo)

If you want to keep the splash screen as it is with your logo, then follow these steps:

- Make a new file in the `src/layouts/components` folder
- Copy the code from the `src/@core/components/spinner/index.tsx` file and paste it in the file you just made
- Remove our SVG logo and add your logo (you can add the logo of any format viz. JPEG, PNG, SVG, etc.)
- Pass your component in the `fallback` prop with the `AuthGuard` and `GuestGuard` components in the `src/pages/_app.tsx` file.

```tsx
// src/pages/_app.tsx

import UserSpinner from 'src/layouts/components/UserSpinner'

<GuestGuard fallback={<UserSpinner />}>{children}</GuestGuard>
<AuthGuard fallback={<UserSpinner />}>{children}</AuthGuard>
```

If you want to change the whole splash screen, then follow these steps:

- Make your own loader component in the `src/layouts/components` folder
- Pass your component in the `fallback` prop with the `AuthGuard` and `GuestGuard` components in the `src/pages/_app.tsx` file.

```tsx
// src/pages/_app.tsx

import UserSpinner from 'src/layouts/components/UserSpinner'

<GuestGuard fallback={<UserSpinner />}>{children}</GuestGuard>
<AuthGuard fallback={<UserSpinner />}>{children}</AuthGuard>
```

You can also pass `null` instead of a loader if you don't want to show a loader in the splash screen.
