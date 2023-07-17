---
sidebarDepth: 2
---

# Layout Overrides

## Overview

The `src/layouts` folder in the root of the `src` folder is for users to override layouts built in the `src/@core` folder. It is highly recommended to override layouts in the `src/layouts` folder instead of directly working in the `src/@core` folder. This will ease your updates to newer versions without facing any hassle of backing up your current code, else it will override your changes in the `src/@core` folder each time you take an update.

Most of the layout components explained on this page are overridden in the `src/layouts/UserLayout.tsx` file.

## Layout PropTypes

Following is the PropTypes for Vertical and Horizontal Layouts only.

```ts
export type LayoutProps = {
  hidden: boolean
  settings: Settings
  children: ReactNode
  scrollToTop?: (props?: any) => ReactNode
  saveSettings: (values: Settings) => void
  footerProps?: {
    sx?: SxProps<Theme>
    content?: (props?: any) => ReactNode
  }
  horizontalLayoutProps?: {
    appBar?: {
      componentProps?: AppBarProps
      content?: (props?: any) => ReactNode
      branding?: (props?: any) => ReactNode
    }
    navMenu?: {
      sx?: SxProps<Theme>
      navItems?: HorizontalNavItemsType
      content?: (props?: any) => ReactNode
    }
  }
  verticalLayoutProps: {
    appBar?: {
      componentProps?: AppBarProps
      content?: (props?: any) => ReactNode
    }
    navMenu: {
      lockedIcon?: ReactNode
      unlockedIcon?: ReactNode
      navItems?: VerticalNavItemsType
      content?: (props?: any) => ReactNode
      branding?: (props?: any) => ReactNode
      afterContent?: (props?: any) => ReactNode
      beforeContent?: (props?: any) => ReactNode
      componentProps?: Omit<SwipeableDrawerProps, 'open' | 'onOpen' | 'onClose'>
    }
  }
}
```

## Vertical Layout

You can override the following layout components:

<!-- no toc -->
- [App Logo](#_1-app-logo)
- [Menu collapse icons](#_2-menu-collapse-icons)
- [Menu content](#_3-menu-content)
- [Add content before menu items](#_4-add-content-before-menu-items)
- [Add content after menu items](#_5-add-content-after-menu-items)
- [Hide menu based on screen size](#_6-hide-menu-based-on-screen-size)
- [Navbar (or AppBar) Content](#_7-navbar-or-appbar-content)
- [Footer content](#_8-footer-content)
- [How to add custom styles](#_9-how-to-add-custom-styles)

### 1. App Logo

If you want to change the app logo, you need to use the `verticalLayoutProps` prop with the `Layout` component and the type accepted by this prop is:

```ts
verticalLayoutProps: {
  navMenu: {
    branding?: (props?: any) => ReactNode
  }
}
```

Here is the code to change the app logo:

<code-group>
<code-block title="TSX" active>
```tsx{25-29}
import { ReactNode } from 'react'
import Box from '@mui/material/Box'
import Typography from '@mui/material/Typography'
import Layout from 'src/@core/layouts/Layout'

interface Props {
  children: ReactNode
}

const AppBrand = () => {
  return (
    <Box sx={{ display: 'flex', alignItems: 'center' }}>
      <img src='...' alt='logo' width='30' height='30' />
      <Typography variant='h6' sx={{ ml: 2 }}>
        React
      </Typography>
    </Box>
  )
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          branding: () => <AppBrand />
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```JSX{20-24}
import Box from '@mui/material/Box'
import Typography from '@mui/material/Typography'
import Layout from 'src/@core/layouts/Layout'

const AppBrand = () => {
  return (
    <Box sx={{ display: 'flex', alignItems: 'center' }}>
      <img src='...' alt='logo' width='30' height='30' />
      <Typography variant='h6' sx={{ ml: 2 }}>
        React
      </Typography>
    </Box>
  )
}

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          branding: () => <AppBrand />
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

Result:

<img alt='override-app-brand' class='medium-zoom' :src="$withBase('/images/layouts/user-override-vertical-app-brand.png')" />

::: warning NOTE
When you override the app logo and when the menu is collapsed, `padding-left` of the menu header will reduce to 0. To center align your logo, you need to manually add `margin-left` to your overridden logo.
:::

### 2. Menu collapse icons

If you want to change the icons for collapsing the vertical menu, you need to use the `verticalLayoutProps` prop with the `Layout` component and the type accepted by this prop is:

```ts
verticalLayoutProps: {
  navMenu: {
    lockedIcon?: ReactNode
    unlockedIcon?: ReactNode
  }
}
```

Here is the code to change the icons for collapsing the vertical menu:

<code-group>
<code-block title="TSX" active>
```tsx{14-19}
import { ReactNode } from 'react'
import Icon from 'src/@core/components/icon'
import Layout from 'src/@core/layouts/Layout'

interface Props {
  children: ReactNode
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          lockedIcon: <Icon icon='bx:left-arrow-alt' />,
          unlockedIcon: <Icon icon='bx:right-arrow-alt' />
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{9-14}
import Icon from 'src/@core/components/icon'
import Layout from 'src/@core/layouts/Layout'

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          lockedIcon: <Icon icon='bx:left-arrow-alt' />,
          unlockedIcon: <Icon icon='bx:right-arrow-alt' />
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

Result of `lockedIcon`:

<img height='400' class='medium-zoom' alt='override-menu-locked' :src="$withBase('/images/layouts/user-override-menu-locked.png')" />

Result of `unlockedIcon`:

<img height='400' class='medium-zoom' alt='override-menu-unlocked' :src="$withBase('/images/layouts/user-override-menu-unlocked.png')" />

### 3. Menu content

If you want to change the menu content, you need to use the `verticalLayoutProps` prop with the `Layout` component and the type accepted by this prop is:

```tsx
verticalLayoutProps: {
  navMenu: {
    content?: (props?: any) => ReactNode
  }
}
```

Here is the code to change the menu content:

<code-group>
<code-block title="TSX" active>
```tsx{24-28}
import { ReactNode } from 'react'
import Layout from 'src/@core/layouts/Layout'

interface Props {
  children: ReactNode
}

const Menu = () => {
  return (
    <ul>
      <li>Menu Item 1</li>
      <li>Menu Item 2</li>
      <li>Menu Item 3</li>
      <li>Menu Item 4</li>
      <li>Menu Item 5</li>
    </ul>
  )
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          content: () => <Menu />
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{19-23}
import Layout from 'src/@core/layouts/Layout'

const Menu = () => {
  return (
    <ul>
      <li>Menu Item 1</li>
      <li>Menu Item 2</li>
      <li>Menu Item 3</li>
      <li>Menu Item 4</li>
      <li>Menu Item 5</li>
    </ul>
  )
}

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          content: () => <Menu />
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

Result:

<img alt='override-menu' class='medium-zoom' :src="$withBase('/images/layouts/user-override-vertical-menu.png')" />

### 4. Add content before menu items

If you want to add something before the menu items, you need to use the `verticalLayoutProps` prop with the `Layout` component and the type accepted by this prop is:

```tsx
verticalLayoutProps: {
  navMenu: {
    beforeContent?: (props?: any) => ReactNode
  }
}
```

Here is the code to add user info before the menu items:

<code-group>
<code-block title="TSX" active>
```tsx{50-54}
import { ReactNode } from 'react'
import Box from '@mui/material/Box'
import Badge from '@mui/material/Badge'
import Avatar from '@mui/material/Avatar'
import { styled } from '@mui/material/styles'
import Typography from '@mui/material/Typography'
import Layout from 'src/@core/layouts/Layout'

interface Props {
  children: ReactNode
}

const User = () => {
  const BadgeContentSpan = styled('span')(({ theme }) => ({
    width: 8,
    height: 8,
    borderRadius: '50%',
    backgroundColor: theme.palette.success.main,
    boxShadow: `0 0 0 2px ${theme.palette.background.paper}`
  }))

  return (
    <Box sx={{ mb: 2, pb: 3, px: 8, borderBottom: theme => `1px solid ${theme.palette.divider}` }}>
      <Box sx={{ display: 'flex', alignItems: 'center' }}>
        <Badge
          overlap='circular'
          badgeContent={<BadgeContentSpan />}
          anchorOrigin={{
            vertical: 'bottom',
            horizontal: 'right'
          }}
        >
          <Avatar src='...' alt='John Doe' sx={{ width: '2.5rem', height: '2.5rem' }} />
        </Badge>
        <Box sx={{ display: 'flex', ml: 3, alignItems: 'flex-start', flexDirection: 'column' }}>
          <Typography sx={{ fontWeight: 600 }}>John Doe</Typography>
          <Typography variant='body2' sx={{ fontSize: '0.8rem', color: 'text.disabled' }}>
            Admin
          </Typography>
        </Box>
      </Box>
    </Box>
  )
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          beforeContent: () => <User />
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{45-49}
import Box from '@mui/material/Box'
import Badge from '@mui/material/Badge'
import Avatar from '@mui/material/Avatar'
import { styled } from '@mui/material/styles'
import Typography from '@mui/material/Typography'
import Layout from 'src/@core/layouts/Layout'

const User = () => {
  const BadgeContentSpan = styled('span')(({ theme }) => ({
    width: 8,
    height: 8,
    borderRadius: '50%',
    backgroundColor: theme.palette.success.main,
    boxShadow: `0 0 0 2px ${theme.palette.background.paper}`
  }))

  return (
    <Box sx={{ mb: 2, pb: 3, px: 8, borderBottom: theme => `1px solid ${theme.palette.divider}` }}>
      <Box sx={{ display: 'flex', alignItems: 'center' }}>
        <Badge
          overlap='circular'
          badgeContent={<BadgeContentSpan />}
          anchorOrigin={{
            vertical: 'bottom',
            horizontal: 'right'
          }}
        >
          <Avatar src='...' alt='John Doe' sx={{ width: '2.5rem', height: '2.5rem' }} />
        </Badge>
        <Box sx={{ display: 'flex', ml: 3, alignItems: 'flex-start', flexDirection: 'column' }}>
          <Typography sx={{ fontWeight: 600 }}>John Doe</Typography>
          <Typography variant='body2' sx={{ fontSize: '0.8rem', color: 'text.disabled' }}>
            Admin
          </Typography>
        </Box>
      </Box>
    </Box>
  )
}

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          beforeContent: () => <User />
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

Result:

<img alt='add-content-before-menu-items' class='medium-zoom' :src="$withBase('/images/layouts/user-add-content-before-menu-items.png')" />

### 5. Add content after menu items

If you want to add something after the menu items, you need to use the `verticalLayoutProps` prop with the `Layout` component and the type accepted by this prop is:

```tsx
verticalLayoutProps: {
  navMenu: {
    afterContent?: (props?: any) => ReactNode
  }
}
```

Here is the code to add menu footer info after the menu items:

<code-group>
<code-block title="TSX" active>
```tsx{28-32}
import { ReactNode } from 'react'
import Box from '@mui/material/Box'
import Layout from 'src/@core/layouts/Layout'

interface Props {
  children: ReactNode
}

const MenuFooter = () => {
  return (
    <Box
      sx={{
        pt: 4,
        display: 'flex',
        justifyContent: 'center',
        borderTop: theme => `1px solid ${theme.palette.divider}`
      }}
    >
      <img src='...' width='...' height='...' alt='menu-footer' />
    </Box>
  )
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          afterContent: () => <MenuFooter />
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{23-27}
import Box from '@mui/material/Box'
import Layout from 'src/@core/layouts/Layout'

const MenuFooter = () => {
  return (
    <Box
      sx={{
        pt: 4,
        display: 'flex',
        justifyContent: 'center',
        borderTop: theme => `1px solid ${theme.palette.divider}`
      }}
    >
      <img src='...' width='...' height='...' alt='menu-footer' />
    </Box>
  )
}

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          afterContent: () => <MenuFooter />
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

Result:

<img alt='add-content-after-menu-items' class='medium-zoom' :src="$withBase('/images/layouts/user-add-content-after-menu-items.png')" />

### 6. Hide menu based on screen size

The `hidden` prop is used to hide the vertical menu at a given screen size. The menu will only be accessible from the Hamburger menu icon which is known as the Vertical Overlay Menu. You can change the screen size from which you want to hide the vertical menu.

In the example below, the vertical menu is visible above the `lg` breakpoint and on screen size below the `lg` breakpoint, it will change to the vertical overlay menu which can be accessed from the Hamburger menu icon.

```tsx
const hidden = useMediaQuery((theme: Theme) => theme.breakpoints.down('lg'))
```

You can also change its value using a specific screen size:

```tsx
const hidden = useMediaQuery('(max-width:1365px)')
```

### 7. Navbar (or AppBar) Content

The content in the appBar comes from the user side itself and thus, it would be very easy and convenient for you to change anything in the appBar. You just have to change the code in the `src/layouts/components/vertical/AppBarContent.tsx` file as per your requirements. The appBar component is then passed in the `verticalLayoutProps` prop with the `Layout` component and the type accepted by this prop is:

```tsx
verticalLayoutProps: {
  appBar?: {
    content?: (props?: any) => ReactNode
  }
}
```

Here is the code to change the appBar:

<code-group>
<code-block title="TSX" active>
```tsx
// src/layouts/components/vertical/AppBarContent.tsx

import Box from '@mui/material/Box'
import IconButton from '@mui/material/IconButton'
import { Settings } from 'src/@core/context/settingsContext'
import Icon from 'src/@core/components/icon'
import ModeToggler from 'src/@core/layouts/components/shared-components/ModeToggler'
import UserDropdown from 'src/@core/layouts/components/shared-components/UserDropdown'

interface Props {
  hidden: boolean
  settings: Settings
  toggleNavVisibility: () => void
  saveSettings: (values: Settings) => void
}

const AppBarContent = (props: Props) => {
  const { hidden, settings, saveSettings, toggleNavVisibility } = props

  return (
    <Box sx={{ width: '100%', display: 'flex', alignItems: 'center', justifyContent: 'space-between' }}>
      <Box className='actions-left' sx={{ mr: 2, display: 'flex', alignItems: 'center' }}>
        {hidden ? (
          <IconButton color='inherit' sx={{ ml: -2.75 }} onClick={toggleNavVisibility}>
            <Icon icon='bx:menu' />
          </IconButton>
        ) : null}
        <ModeToggler settings={settings} saveSettings={saveSettings} />
      </Box>
      <UserDropdown settings={settings} />
    </Box>
  )
}

export default AppBarContent
```
</code-block>

<code-block title="JSX">
```jsx
// src/layouts/components/vertical/AppBarContent.js

import Box from '@mui/material/Box'
import IconButton from '@mui/material/IconButton'
import Icon from 'src/@core/components/icon'
import ModeToggler from 'src/@core/layouts/components/shared-components/ModeToggler'
import UserDropdown from 'src/@core/layouts/components/shared-components/UserDropdown'

const AppBarContent = props => {
  const { hidden, settings, saveSettings, toggleNavVisibility } = props

  return (
    <Box sx={{ width: '100%', display: 'flex', alignItems: 'center', justifyContent: 'space-between' }}>
      <Box className='actions-left' sx={{ mr: 2, display: 'flex', alignItems: 'center' }}>
        {hidden ? (
          <IconButton color='inherit' sx={{ ml: -2.75 }} onClick={toggleNavVisibility}>
            <Icon icon='bx:menu' />
          </IconButton>
        ) : null}
        <ModeToggler settings={settings} saveSettings={saveSettings} />
      </Box>
      <UserDropdown settings={settings} />
    </Box>
  )
}

export default AppBarContent
```
</code-block>
</code-group>

<code-group>
<code-block title="TSX" active>
```tsx{8,21-32}
// src/layouts/UserLayout.tsx

import { ReactNode } from 'react'
import { Theme } from '@mui/material/styles'
import useMediaQuery from '@mui/material/useMediaQuery'
import Layout from 'src/@core/layouts/Layout'
import { useSettings } from 'src/@core/hooks/useSettings'
import VerticalAppBarContent from 'src/layouts/components/vertical/AppBarContent'

interface Props {
  children: ReactNode
}

const UserLayout = ({ children }: Props) => {
  const { settings, saveSettings } = useSettings()
  const hidden = useMediaQuery((theme: Theme) => theme.breakpoints.down('lg'))

  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        appBar: {
          content: props => (
            <VerticalAppBarContent
              hidden={hidden}
              settings={settings}
              saveSettings={saveSettings}
              toggleNavVisibility={props.toggleNavVisibility}
            />
          )
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{6,15-26}
// src/layouts/UserLayout.js

import useMediaQuery from '@mui/material/useMediaQuery'
import Layout from 'src/@core/layouts/Layout'
import { useSettings } from 'src/@core/hooks/useSettings'
import VerticalAppBarContent from 'src/layouts/components/vertical/AppBarContent'

const UserLayout = ({ children }) => {
  const { settings, saveSettings } = useSettings()
  const hidden = useMediaQuery(theme => theme.breakpoints.down('lg'))

  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        appBar: {
          content: props => (
            <VerticalAppBarContent
              hidden={hidden}
              settings={settings}
              saveSettings={saveSettings}
              toggleNavVisibility={props.toggleNavVisibility}
            />
          )
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

Result:

<img alt='override-appBar' class='medium-zoom' :src="$withBase('/images/layouts/user-override-vertical-appBar.png')" />

### 8. Footer content

If you want to change the footer content, you need to use the `footerProps` prop with the `Layout` component and the type accepted by this prop is:

```tsx
footerProps?: {
  content?: (props?: any) => ReactNode
}
```

Here is the code to change the footer content:

<code-group>
<code-block title="TSX" active>
```tsx{12-14}
import { ReactNode } from 'react'
import Layout from 'src/@core/layouts/Layout'

interface Props {
  children: ReactNode
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      footerProps={{
        content: () => 'I am footer which is overridden by the user'
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{7-9}
import Layout from 'src/@core/layouts/Layout'

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // other props
      footerProps={{
        content: () => 'I am footer which is overridden by the user'
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

Result:

<img alt='override-footer' class='medium-zoom' :src="$withBase('/images/layouts/user-override-vertical-footer.png')" />

### 9. How to add custom styles

You can add your custom styles for the whole layout with the help of `footerProps` and `verticalLayoutProps` props with the `Layout` component. The type for the same is:

```ts
footerProps?: {
  sx?: SxProps<Theme>
}
verticalLayoutProps: {
  appBar?: {
    componentProps?: AppBarProps
  }
  navMenu: {
    componentProps?: Omit<SwipeableDrawerProps, 'open' | 'onOpen' | 'onClose'>
  }
}
```

Refer to the following example for adding your custom styles:

<code-group>
<code-block title="TSX" active>
```tsx{12-26}
import { ReactNode } from 'react'
import Layout from 'src/@core/layouts/Layout'

interface Props {
  children: ReactNode
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      footerProps={{
        sx: { p: 5, backgroundColor: theme => theme.palette.background.paper }
      }},
      verticalLayoutProps={{
        navMenu: {
          componentProps: {
            sx: { '& .nav-header': { borderBottom: theme => `1px solid ${theme.palette.divider}` } }
          },
          appBar: {
            componentProps: {
              sx: { boxShadow: theme => theme.shadows[9] }
            }
          }
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{7-21}
import Layout from 'src/@core/layouts/Layout'

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // other props
      footerProps={{
        sx: { p: 5, backgroundColor: theme => theme.palette.background.paper }
      }},
      verticalLayoutProps={{
        navMenu: {
          componentProps: {
            sx: { '& .nav-header': { borderBottom: theme => `1px solid ${theme.palette.divider}` } }
          },
          appBar: {
            componentProps: {
              sx: { boxShadow: theme => theme.shadows[9] }
            }
          }
        }
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

## Horizontal Layout

::: danger Important!
As mentioned [here](/guide/layout/navigation-menu-structure.html#horizontal-navigation-structure), you need to add all the necessary items for the Vertical Layout. Please follow [these steps](/guide/layout/layout-overrides.html#vertical-layout) to add items for the Vertical Layout and then follow the steps explained below.
:::

You can override the following layout components:

<!-- no toc -->
- [App Logo](#_1-app-logo-2)
- [Menu content](#_2-menu-content)
- [Hide menu based on screen size](#_3-hide-menu-based-on-screen-size)
- [AppBar Content](#_4-appbar-content)
- [Footer content](#_5-footer-content)
- [How to add custom styles](#_6-how-to-add-custom-styles)

### 1. App Logo

If you want to change the app logo, you need to use the `verticalLayoutProps` and `horizontalLayoutProps` props with the `Layout` component and the type accepted by these props is:

```tsx
verticalLayoutProps: {
  navMenu: {
    branding?: (props?: any) => ReactNode
  }
}
horizontalLayoutProps?: {
  appBar?: {
    branding?: (props?: any) => ReactNode
  }
}
```

Here is the code to change the app logo:

<code-group>
<code-block title="TSX" active>
```tsx{25-36}
import { ReactNode } from 'react'
import Box from '@mui/material/Box'
import Typography from '@mui/material/Typography'
import Layout from 'src/@core/layouts/Layout'

interface Props {
  children: ReactNode
}

const AppBrand = () => {
  return (
    <Box sx={{ display: 'flex', alignItems: 'center' }}>
      <img src='...' alt='logo' width='30' height='30' />
      <Typography variant='h6' sx={{ ml: 2 }}>
        React
      </Typography>
    </Box>
  )
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          branding: () => <AppBrand />
        }
      }}
      {...(settings.layout === 'horizontal' && {
        horizontalLayoutProps: {
          appBar: {
            branding: () => <AppBrand />
          }
        }
      })}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{20-31}
import Box from '@mui/material/Box'
import Typography from '@mui/material/Typography'
import Layout from 'src/@core/layouts/Layout'

const AppBrand = () => {
  return (
    <Box sx={{ display: 'flex', alignItems: 'center' }}>
      <img src='...' alt='logo' width='30' height='30' />
      <Typography variant='h6' sx={{ ml: 2 }}>
        React
      </Typography>
    </Box>
  )
}

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          branding: () => <AppBrand />
        }
      }}
      {...(settings.layout === 'horizontal' && {
        horizontalLayoutProps: {
          appBar: {
            branding: () => <AppBrand />
          }
        }
      })}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

Result:

<img alt='override-app-brand' class='medium-zoom' :src="$withBase('/images/layouts/user-override-horizontal-app-brand.png')" />

### 2. Menu content

If you want to change the menu content, you need to use the `verticalLayoutProps` and `horizontalLayoutProps` props with the `Layout` component and the type accepted by these props is:

```tsx
verticalLayoutProps: {
  navMenu: {
    content?: (props?: any) => ReactNode
  }
}
horizontalLayoutProps?: {
  navMenu: {
    content?: (props?: any) => ReactNode
  }
}
```

Here is the code to change the menu content:

<code-group>
<code-block title="TSX" active>
```tsx{24-35}
import { ReactNode } from 'react'
import Layout from 'src/@core/layouts/Layout'

interface Props {
  children: ReactNode
}

const Menu = () => {
  return (
    <ul>
      <li>Menu Item 1</li>
      <li>Menu Item 2</li>
      <li>Menu Item 3</li>
      <li>Menu Item 4</li>
      <li>Menu Item 5</li>
    </ul>
  )
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          content: () => <Menu />
        }
      }}
      {...(settings.layout === 'horizontal' && {
        horizontalLayoutProps: {
          navMenu: {
            content: () => 'I am menu which is overridden by the user'
          }
        }
      })}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```tsx{19-30}
import Layout from 'src/@core/layouts/Layout'

const Menu = () => {
  return (
    <ul>
      <li>Menu Item 1</li>
      <li>Menu Item 2</li>
      <li>Menu Item 3</li>
      <li>Menu Item 4</li>
      <li>Menu Item 5</li>
    </ul>
  )
}

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        navMenu: {
          content: () => <Menu />
        }
      }}
      {...(settings.layout === 'horizontal' && {
        horizontalLayoutProps: {
          navMenu: {
            content: () => 'I am menu which is overridden by the user'
          }
        }
      })}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

Result:

<img alt='override-menu' class='medium-zoom' :src="$withBase('/images/layouts/user-override-horizontal-menu.png')" />

### 3. Hide menu based on screen size

The `hidden` prop is used to hide the horizontal menu at a given screen size. The menu will only be accessible from the Hamburger menu icon which is known as the Vertical Overlay Menu. You can change the screen size from which you want to hide the horizontal menu.

In the example below, the horizontal menu is visible above the `lg` breakpoint and on screen size below the `lg` breakpoint, it will change to the vertical overlay menu which can be accessed from the Hamburger menu icon.

```tsx
const hidden = useMediaQuery((theme: Theme) => theme.breakpoints.down('lg'))
```

You can also change its value using a specific screen size:

```tsx
const hidden = useMediaQuery('(max-width:1365px)')
```

### 4. AppBar Content

The content in the appBar which is on the right side comes from the user side itself and thus, it would be very easy and convenient for you to change anything in the appBar. You just have to change the code in the `src/layouts/components/horizontal/AppBarContent.tsx` file. The appBar component is then passed in the `horizontalLayoutProps` prop with the `Layout` component. The appBar component for the Vertical Layout (which comes from the `src/layouts/components/vertical/AppBarContent.tsx` file) is passed in the `verticalLayoutProps` prop with the `Layout` component.

The type accepted by these props is:

```tsx
verticalLayoutProps: {
  appBar?: {
    content?: (props?: any) => ReactNode
  }
}
horizontalLayoutProps?: {
  appBar?: {
    content?: (props?: any) => ReactNode
  }
}
```

Suppose you need the app logo, navigation menu as well as some actions in one line, then you need to follow the steps given below.

Firstly, you need to hide the navigation menu section which is below the appBar from the `src/configs/themeConfig.ts` file:

<code-group>
<code-block title="TS" active>
```ts{5}
// src/configs/themeConfig.ts

const themeConfig: ThemeConfig = {
  ...,
  navHidden: true,
  ...
}
```
</code-block>

<code-block title="JS">
```js{5}
// src/configs/themeConfig.js

const themeConfig = {
  ...,
  navHidden: true,
  ...
}
```
</code-block>
</code-group>

Then you need to change the appBar accordingly:

<code-group>
<code-block title="TSX" active>
```tsx
// src/layouts/components/horizontal/AppBarContent.tsx

import Box from '@mui/material/Box'
import { Settings } from 'src/@core/context/settingsContext'
import { HorizontalNavItemsType } from 'src/@core/layouts/types'
import Navigation from 'src/@core/layouts/components/horizontal/navigation'
import UserDropdown from 'src/@core/layouts/components/shared-components/UserDropdown'

interface Props {
  settings: Settings
  horizontalNavItems?: HorizontalNavItemsType
}

const AppBarContent = (props: Props) => {
  const { settings, horizontalNavItems } = props

  return (
    <Box sx={{ width: '100%', display: 'flex', alignItems: 'center', justifyContent: 'space-between' }}>
      <Navigation settings={settings} horizontalNavItems={horizontalNavItems} />
      <UserDropdown settings={settings} />
    </Box>
  )
}

export default AppBarContent
```
</code-block>

<code-block title="JSX">
```jsx
// src/layouts/components/horizontal/AppBarContent.js

import Box from '@mui/material/Box'
import Navigation from 'src/@core/layouts/components/horizontal/navigation'
import UserDropdown from 'src/@core/layouts/components/shared-components/UserDropdown'

const AppBarContent = props => {
  const { settings, horizontalNavItems } = props

  return (
    <Box sx={{ width: '100%', display: 'flex', alignItems: 'center', justifyContent: 'space-between' }}>
      <Navigation settings={settings} horizontalNavItems={horizontalNavItems} />
      <UserDropdown settings={settings} />
    </Box>
  )
}

export default AppBarContent
```
</code-block>
</code-group>

Then you need to pass that component in the `horizontalLayoutProps` prop with the `Layout` component:

<code-group>
<code-block title="TSX" active>
```tsx{6-8,19-39}
// src/layouts/UserLayout.tsx

import { ReactNode } from 'react'
import Layout from 'src/@core/layouts/Layout'
import { useSettings } from 'src/@core/hooks/useSettings'
import HorizontalNavItems from 'src/navigation/horizontal'
import VerticalAppBarContent from './components/vertical/AppBarContent'
import HorizontalAppBarContent from './components/horizontal/AppBarContent'

interface Props {
  children: ReactNode
}

const UserLayout = ({ children }: Props) => {
  const { settings } = useSettings()
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        appBar: {
          content: props => (
            <VerticalAppBarContent
              hidden={hidden}
              settings={settings}
              saveSettings={saveSettings}
              toggleNavVisibility={props.toggleNavVisibility}
            />
          )
        }
      }}
      {...(settings.layout === 'horizontal' && {
        horizontalLayoutProps: {
          appBar: {
            content: () => (
              <HorizontalAppBarContent settings={settings} horizontalNavItems={HorizontalNavItems()} />
            )
          }
        }
      })}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{5-7,14-34}
// src/layouts/UserLayout.js

import Layout from 'src/@core/layouts/Layout'
import { useSettings } from 'src/@core/hooks/useSettings'
import HorizontalNavItems from 'src/navigation/horizontal'
import VerticalAppBarContent from './components/vertical/AppBarContent'
import HorizontalAppBarContent from './components/horizontal/AppBarContent'

const UserLayout = ({ children }) => {
  const { settings } = useSettings()
  return (
    <Layout
      {...} // other props
      verticalLayoutProps={{
        appBar: {
          content: props => (
            <VerticalAppBarContent
              hidden={hidden}
              settings={settings}
              saveSettings={saveSettings}
              toggleNavVisibility={props.toggleNavVisibility}
            />
          )
        }
      }}
      {...(settings.layout === 'horizontal' && {
        horizontalLayoutProps: {
          appBar: {
            content: () => (
              <HorizontalAppBarContent settings={settings} horizontalNavItems={HorizontalNavItems()} />
            )
          }
        }
      })}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

Result:

<img alt='override-appBar' class='medium-zoom' :src="$withBase('/images/layouts/user-override-horizontal-appBar.png')" />

### 5. Footer content

If you want to change the footer content, you need to use the `footerProps` prop with the `Layout` component and the type accepted by this prop is:

```tsx
footerProps?: {
  content?: (props?: any) => ReactNode
}
```

Here is the code to change the footer content:

<code-group>
<code-block title="TSX" active>
```tsx{12-14}
import { ReactNode } from 'react'
import Layout from 'src/@core/layouts/Layout'

interface Props {
  children: ReactNode
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      footerProps={{
        content: () => 'I am footer which is overridden by the user'
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{7-9}
import Layout from 'src/@core/layouts/Layout'

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // other props
      footerProps={{
        content: () => 'I am footer which is overridden by the user'
      }}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

Result:

<img alt='override-footer' class='medium-zoom' :src="$withBase('/images/layouts/user-override-horizontal-footer.png')" />

### 6. How to add custom styles

You can add your custom styles for the whole layout with the help of `footerProps`, `verticalLayoutProps` and `horizontalLayoutProps` props with the `Layout` component. The type for the same is:

```ts
footerProps?: {
  sx?: SxProps<Theme>
}
verticalLayoutProps: {
  appBar?: {
    componentProps?: AppBarProps
  }
  navMenu: {
    componentProps?: Omit<SwipeableDrawerProps, 'open' | 'onOpen' | 'onClose'>
  }
}
horizontalLayoutProps?: {
  appBar?: {
    componentProps?: AppBarProps
  }
  navMenu?: {
    sx?: SxProps<Theme>
  }
}
```

Refer to the following example for adding your custom styles:

<code-group>
<code-block title="TSX" active>
```tsx{12-42}
import { ReactNode } from 'react'
import Layout from 'src/@core/layouts/Layout'

interface Props {
  children: ReactNode
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      footerProps={{
        sx: { p: 5, backgroundColor: theme => theme.palette.background.paper }
      }},
      verticalLayoutProps={{
        navMenu: {
          componentProps: {
            sx: { '& .nav-header': { borderBottom: theme => `1px solid ${theme.palette.divider}` } }
          },
          appBar: {
            componentProps: {
              sx: { boxShadow: theme => theme.shadows[9] }
            }
          }
        }
      }}
      {...(settings.layout === 'horizontal' && {
        horizontalLayoutProps: {
          appBar: {
            componentProps: {
              sx: { boxShadow: theme => theme.shadows[9] }
            }
          },
          navMenu: {
            sx: {
              '& .menu-content > *:not(:last-child)': {
                pr: 2,
                borderRight: theme => `1px solid ${theme.palette.divider}`
              }
            }
        }
      })}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{7-37}
import Layout from 'src/@core/layouts/Layout'

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // other props
      footerProps={{
        sx: { p: 5, backgroundColor: theme => theme.palette.background.paper }
      }},
      verticalLayoutProps={{
        navMenu: {
          componentProps: {
            sx: { '& .nav-header': { borderBottom: theme => `1px solid ${theme.palette.divider}` } }
          },
          appBar: {
            componentProps: {
              sx: { boxShadow: theme => theme.shadows[9] }
            }
          }
        }
      }}
      {...(settings.layout === 'horizontal' && {
        horizontalLayoutProps: {
          appBar: {
            componentProps: {
              sx: { boxShadow: theme => theme.shadows[9] }
            }
          },
          navMenu: {
            sx: {
              '& .menu-content > *:not(:last-child)': {
                pr: 2,
                borderRight: theme => `1px solid ${theme.palette.divider}`
              }
            }
        }
      })}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

## Blank Layout

If you want to change the Blank Layout, you need to follow these steps:

- Make a new file (let us say `UserBlankLayout.tsx` file name) in the `src/layouts` folder
- Copy the whole code from the `src/@core/layouts/BlankLayout.tsx` file and paste it into the `src/layouts/UserBlankLayout.tsx` file
- Edit the `src/layouts/UserBlankLayout.tsx` file as per your requirements
- Now, to use this layout in any of your pages, you need to do this:

<code-group>
<code-block title="TSX" active>
```tsx{2,10}
import { ReactNode } from 'react'
import UserBlankLayout from 'src/layouts/UserBlankLayout'

const Component = () => {
  return (
    // Your content
  )
}

Component.getLayout = (page: ReactNode) => <UserBlankLayout>{page}</UserBlankLayout>

export default Component
```
</code-block>

<code-block title="JSX">
```jsx{1,9}
import UserBlankLayout from 'src/layouts/UserBlankLayout'

const Component = () => {
  return (
    // Your content
  )
}

Component.getLayout = page => <UserBlankLayout>{page}</UserBlankLayout>

export default Component
```
</code-block>
</code-group>

## Blank Layout with AppBar

If you want to change the navbar, you need to follow these steps:

- Make a new file (let us say `UserBlankLayoutWithAppBar.tsx` file name) in the `src/layouts` folder
- Copy the whole code from the `src/@core/layouts/BlankLayoutWithAppBar.tsx` file and paste it into the `src/layouts/UserBlankLayoutWithAppBar.tsx` file
- Edit the `src/layouts/UserBlankLayoutWithAppBar.tsx` file as per your requirements
- Now, to use this layout in any of your pages, you need to do this:

<code-group>
<code-block title="TSX" active>
```tsx{2,10}
import { ReactNode } from 'react'
import UserBlankLayoutWithAppBar from 'src/layouts/UserBlankLayoutWithAppBar'

const Component = () => {
  return (
    // Your content
  )
}

Component.getLayout = (page: ReactNode) => <UserBlankLayoutWithAppBar>{page}</UserBlankLayoutWithAppBar>

export default Component
```
</code-block>

<code-block title="JSX">
```jsx{1,9}
import UserBlankLayoutWithAppBar from 'src/layouts/UserBlankLayoutWithAppBar'

const Component = () => {
  return (
    // Your content
  )
}

Component.getLayout = page => <UserBlankLayoutWithAppBar>{page}</UserBlankLayoutWithAppBar>

export default Component
```
</code-block>
</code-group>

## Scroll to Top

If you want to change the scroll to top component, you need to use the `scrollToTop` prop with the `Layout` component in the `src/layouts/UserLayout.tsx` file and the type accepted by this prop is:

```tsx
scrollToTop?: (props?: any) => ReactNode
```

Here is the code to change the scroll to top component:

<code-group>
<code-block title="TSX" active>
```tsx{24}
import { ReactNode } from 'react'
import Button from '@mui/material/Button'
import Layout from 'src/@core/layouts/Layout'
import ScrollToTop from 'src/@core/components/scroll-to-top'

interface Props {
  children: ReactNode
}

const UserScrollToTop = () => {
  return (
    <ScrollToTop>
      <Button color='success' variant='contained'>
        Scroll To Top
      </Button>
    </ScrollToTop>
  )
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // other props
      scrollToTop={() => <UserScrollToTop />}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{19}
import Button from '@mui/material/Button'
import Layout from 'src/@core/layouts/Layout'
import ScrollToTop from 'src/@core/components/scroll-to-top'

const UserScrollToTop = () => {
  return (
    <ScrollToTop>
      <Button color='success' variant='contained'>
        Scroll To Top
      </Button>
    </ScrollToTop>
  )
}

const UserLayout = ({ children } => {
  return (
    <Layout
      {...} // other props
      scrollToTop={() => <UserScrollToTop />}
    >
      {children}
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>

Result:

<img alt='override-scroll-to-top' class='medium-zoom' :src="$withBase('/images/layouts/user-override-scroll-to-top.png')" />

## Customizer

If you want to override the customizer or make a custom customizer, then follow these steps:

- Hide the customizer from the `src/configs/themeConfig.ts` file

<code-group>
<code-block title="TS" active>
```ts{5}
// src/configs/themeConfig.ts

const themeConfig: ThemeConfig = {
  ...,
  disableCustomizer: true,
  ...
}
```
</code-block>

<code-block title="JS">
```js{5}
// src/configs/themeConfig.js

const themeConfig = {
  ...,
  disableCustomizer: true,
  ...
}
```
</code-block>
</code-group>

- Make a new file (let us say `Customizer.tsx` file name) in the `src/layouts/components` folder
- Copy the whole code from the `src/@core/components/customizer/index.tsx` file and paste it into the `src/layouts/components/Customizer.tsx` file
- Edit the `src/layouts/components/Customizer.tsx` file as per your requirements
- Render this customizer in the `src/layouts/UserLayout.tsx` file:

<code-group>
<code-block title="TSX" active>
```tsx{5,17}
// src/layouts/UserLayout.tsx

import { ReactNode } from 'react'
import Layout from 'src/@core/layouts/Layout'
import Customizer from 'src/layouts/components/Customizer'

interface Props {
  children: ReactNode
}

const UserLayout = ({ children }: Props) => {
  return (
    <Layout
      {...} // all the props
    >
      {children}
      <Customizer />
    </Layout>
  )
}

export default UserLayout
```
</code-block>

<code-block title="JSX">
```jsx{4,12}
// src/layouts/UserLayout.js

import Layout from 'src/@core/layouts/Layout'
import Customizer from 'src/layouts/components/Customizer'

const UserLayout = ({ children }) => {
  return (
    <Layout
      {...} // all the props
    >
      {children}
      <Customizer />
    </Layout>
  )
}

export default UserLayout
```
</code-block>
</code-group>
