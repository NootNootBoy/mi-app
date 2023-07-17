# Routing

Sneat uses Next.js's file-system based router built on the concept of pages.

When a file is added to the `src/pages` directory, it's automatically available as a route.

## Index routes

The router will automatically route files named index to the root of the directory.

- `pages/index.tsx` → `/`
- `pages/dashboards/index.tsx` → `/blog`

## Nested routes

The router supports nested files. If you create a nested folder structure, files will automatically be routed in the same way.

- `pages/dashboards/ecommerce/index.tsx` → `/dashboards/ecommerce`

## Dynamic route segments

Defining routes by using predefined paths is not always enough for complex applications. In Next.js you can add brackets to a page `param` to create a dynamic route (a.k.a. URL slugs, pretty URLs, and others).

To match a dynamic segment you can use the bracket syntax. This allows you to match named parameters.

- `pages/apps/email/[folder].tsx` → `/apps/email/spam`
- `pages/apps/email/label/[label].tsx` → `/apps/email/label/company`
- `pages/apps/email/[...all].tsx` → `/apps/email/*` (`/apps/email/view/id/1`)
