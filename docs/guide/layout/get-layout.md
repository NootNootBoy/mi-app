# getLayout

::: tip
We recommend you to go through the [Per page Layout Docs of NextJS](https://nextjs.org/docs/basic-features/layouts#per-page-layouts) to understand how the layout works on any single page in the app. Once you understand the layout from NextJS, then you may go through our docs for a better understanding.
:::

## Overview

If you want to change the default layout for a particular page, you can use the `getLayout` method with your component.

## Blank Layout

Here is an example of how to change the layout from default layout to blank layout for any page:

<code-group>
<code-block title="TSX" active>
```tsx{2,10}
import { ReactNode } from 'react'
import BlankLayout from 'src/@core/layouts/BlankLayout'

const Login = () => {
  return {
    /* Your content */
  }
}

Login.getLayout = (page: ReactNode) => <BlankLayout>{page}</BlankLayout>

export default Login
```
</code-block>

<code-block title="JSX">
```jsx{1,9}
import BlankLayout from 'src/@core/layouts/BlankLayout'

const Login = () => {
  return {
    /* Your content */
  }
}

Login.getLayout = page => <BlankLayout>{page}</BlankLayout>

export default Login
```
</code-block>
</code-group>

## Blank Layout with AppBar

Here is an example of how to change the layout from default layout to blank layout with appBar for any page:

<code-group>
<code-block title="TSX" active>
```tsx{2,10}
import { ReactNode } from 'react'
import BlankLayoutWithAppBar from 'src/@core/layouts/BlankLayoutWithAppBar'

const Login = () => {
  return {
    /* Your content */
  }
}

Login.getLayout = (page: ReactNode) => <BlankLayoutWithAppBar>{page}</BlankLayoutWithAppBar>

export default Login
```
</code-block>

<code-block title="JSX">
```jsx{1,9}
import BlankLayoutWithAppBar from 'src/@core/layouts/BlankLayoutWithAppBar'

const Login = () => {
  return {
    /* Your content */
  }
}

Login.getLayout = page => <BlankLayoutWithAppBar>{page}</BlankLayoutWithAppBar>

export default Login
```
</code-block>
</code-group>

## Custom Layout

Refer to the code below to create a blog layout:

<code-group>
<code-block title="TSX" active>
```tsx
import { ReactNode } from 'react'
import Box from '@mui/material/Box'
import Grid from '@mui/material/Grid'
import UserLayout from 'src/layouts/UserLayout'

const SidebarComponent = () => (
  <Box sx={{ px: 4, py: 2, height: 'calc(100vh - 12rem)', backgroundColor: 'background.paper' }}>
    <h1>Sidebar</h1>
  </Box>
)

const BlogLayout = () => <h1>Blogs</h1>

BlogLayout.getLayout = (page: ReactNode) => {
  return (
    <UserLayout>
      <Grid spacing={6} container>
        <Grid item md={9}>
          {page}
        </Grid>
        <Grid item md={3}>
          <SidebarComponent />
        </Grid>
      </Grid>
    </UserLayout>
  )
}

export default BlogLayout
```
</code-block>

<code-block title="JSX">
```jsx
import Box from '@mui/material/Box'
import Grid from '@mui/material/Grid'
import UserLayout from 'src/layouts/UserLayout'

const SidebarComponent = () => (
  <Box sx={{ px: 4, py: 2, height: 'calc(100vh - 12rem)', backgroundColor: 'background.paper' }}>
    <h1>Sidebar</h1>
  </Box>
)

const BlogLayout = () => <h1>Blogs</h1>

BlogLayout.getLayout = page => {
  return (
    <UserLayout>
      <Grid spacing={6} container>
        <Grid item md={9}>
          {page}
        </Grid>
        <Grid item md={3}>
          <SidebarComponent />
        </Grid>
      </Grid>
    </UserLayout>
  )
}

export default BlogLayout
```
</code-block>
</code-group>

Result:

<img alt='blog-layout' class='medium-zoom' :src="$withBase('/images/layouts/blog-layout.png')" />

## Change the default page layout

Suppose, you want to change the default page layout for all the pages in your project, then follow the below steps:

- Make a layout as per your requirements in the `src/layouts` folder (let us assume that you named the file as `UserDefaultLayout.tsx`)
- Import the newly created file in the `src/pages/_app.tsx` file as:

```tsx
import UserDefaultLayout from 'src/layouts/UserDefaultLayout'
```

- Change the `getLayout` variable

**from**

```tsx
const getLayout = Component.getLayout ?? (page => <UserLayout contentHeightFixed={contentHeightFixed}>{page}</UserLayout>)
```

**to**

```tsx
const getLayout = Component.getLayout ?? (page => <UserDefaultLayout>{page}</UserDefaultLayout>)
```
