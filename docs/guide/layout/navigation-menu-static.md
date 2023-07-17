# Static Navigation Menu

## Overview

On this page, you will understand how to use a static navigation menu in Vertical layout as well as in Horizontal layout.

## Vertical layout

To use the static navigation menu in the Vertical layout, follow these steps:

- You need to write all of your navigation section titles, navigation groups and navigation links in [this](/guide/layout/navigation-menu-structure.html#vertical-navigation-structure) structure in the `src/navigation/vertical/index.ts` file
- And then import `src/navigation/vertical/index.ts` file in `src/layouts/UserLayout.tsx` file and pass it as shown below:

<code-group>
<code-block title="TSX" active>
```tsx{5,15-19}
// src/layouts/UserLayout.tsx

import { ReactNode } from 'react'
import Layout from 'src/@core/layouts/Layout'
import VerticalNavItems from 'src/navigation/vertical'

interface Props {
  children: ReactNode
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          navItems: VerticalNavItems()
        }
      }}
    >
      {children}
    </Layout>
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{4,10-14}
// src/layouts/UserLayout.js

import Layout from 'src/@core/layouts/Layout'
import VerticalNavItems from 'src/navigation/vertical'

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          navItems: VerticalNavItems()
        }
      }}
    >
      {children}
    </Layout>
}

export default UserLayout
```
</code-block>
</code-group>

## Horizontal layout

::: danger Important!
As mentioned [here](/guide/layout/navigation-menu-structure.html#horizontal-navigation-structure), you need to add menu items for Vertical Navigation as well. Please follow [these steps](/guide/layout/navigation-menu-static.html#vertical-layout) to add the Vertical Navigation and then follow the steps explained below.
:::

To use the static navigation menu in the Horizontal layout, follow these steps:

- You need to write all of your navigation groups and navigation links in [this](/guide/layout/navigation-menu-structure.html#horizontal-navigation-structure) structure in the `src/navigation/horizontal/index.ts` file
- And then import `src/navigation/horizontal/index.ts` file in `src/layouts/UserLayout.tsx` file and pass it as shown below:

<code-group>
<code-block title="TSX" active>
```tsx{5-6,16-27}
// src/layouts/UserLayout.tsx

import { ReactNode } from 'react'
import Layout from 'src/@core/layouts/Layout'
import VerticalNavItems from 'src/navigation/vertical'
import HorizontalNavItems from 'src/navigation/horizontal'

interface Props {
  children: ReactNode
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          navItems: VerticalNavItems()
        }
      }}
      {...(settings.layout === 'horizontal' && {
        horizontalLayoutProps: {
          navMenu: {
            navItems: HorizontalNavItems()
          }
        }
      })}
    >
      {children}
    </Layout>
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{4-5,11-22}
// src/layouts/UserLayout.tsx

import Layout from 'src/@core/layouts/Layout'
import VerticalNavItems from 'src/navigation/vertical'
import HorizontalNavItems from 'src/navigation/horizontal'

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          navItems: VerticalNavItems()
        }
      }}
      {...(settings.layout === 'horizontal' && {
        horizontalLayoutProps: {
          navMenu: {
            navItems: HorizontalNavItems()
          }
        }
      })}
    >
      {children}
    </Layout>
}

export default UserLayout
```
</code-block>
</code-group>
