---
sidebarDepth: 2
---

# Navigation Menu Structure

## Overview

While creating the navigation menu, you need to know the structure of it. On this page, you will understand how to create a navigation section title (which is only in the vertical navigation menu), navigation group and navigation link.

## Vertical Navigation Structure

Following are the items that you can create for your vertical navigation:

- [Navigation Section Header](#_1-navigation-section-header)
- [Navigation Group](#_2-navigation-group)
- [Navigation Link](#_3-navigation-link)

### 1. Navigation Section Header

It is used to group some navigation groups and/or navigation links in some sections. This is only used in the vertical navigation menu. To create a navigation section, you need to add an object with the following structure:

```ts
type NavSectionTitle = {
  action?: string
  subject?: string
  sectionTitle: string
}
```

Here is the example code:

```ts
{
  sectionTitle: 'Apps & Pages'
}
```

Result:

<img height='200' class='medium-zoom' alt='navigation-section-header' :src="$withBase('/images/layouts/navigation-section-header.png')" />

### 2. Navigation Group

It is used to group some navigation groups and/or navigation links that can be treated as an accordion or a collapse. To create a navigation group, you need to add an object with the following structure:

```ts
// For Static Navigation Menu
type NavGroup = {
  title: string
  action?: string
  subject?: string
  badgeContent?: string
  children?: (NavGroup | NavLink)[]
  icon?: string | string[] | ReactNode
  badgeColor?: 'default' | 'primary' | 'secondary' | 'success' | 'error' | 'warning' | 'info'
}

// For Server Side Navigation Menu
type NavGroup = {
  icon?: string
  title: string
  action?: string
  subject?: string
  badgeContent?: string
  children?: (NavGroup | NavLink)[]
  badgeColor?: 'default' | 'primary' | 'secondary' | 'success' | 'error' | 'warning' | 'info'
}
```

Here is the example code:

<code-group>
<code-block title="TS" active>
```ts
import { VerticalNavItemsType } from 'src/@core/layouts/types'

const navigation = (): VerticalNavItemsType => {
  return [
    {
      badgeContent: '3',
      title: 'Components',
      icon: 'mdi:archive-outline',
      badgeColor: 'success',
      children: [
        {
          title: 'Accordion',
          path: '/components/accordion'
        },
        {
          title: 'Cards',
          children: [
            {
              title: 'Basic',
              path: '/components/cards/basic'
            },
            {
              title: 'Advanced',
              path: '/components/cards/advanced'
            }
          ]
        },
        {
          title: 'Chips',
          path: '/components/chips'
        }
      ]
    }
  ]
}

export default navigation
```
</code-block>

<code-block title="JS">
```js
const navigation = () => {
  return [
    {
      badgeContent: '3',
      title: 'Components',
      icon: 'mdi:archive-outline',
      badgeColor: 'success',
      children: [
        {
          title: 'Accordion',
          path: '/components/accordion'
        },
        {
          title: 'Cards',
          children: [
            {
              title: 'Basic',
              path: '/components/cards/basic'
            },
            {
              title: 'Advanced',
              path: '/components/cards/advanced'
            }
          ]
        },
        {
          title: 'Chips',
          path: '/components/chips'
        }
      ]
    }
  ]
}

export default navigation
```
</code-block>
</code-group>

Result:

<img alt='navigation-group' class='medium-zoom' :src="$withBase('/images/layouts/navigation-vertical-group.png')" />

### 3. Navigation Link

To create a navigation link, you need to add an object with the following structure:

```ts
// For Static Navigation Menu
type NavLink = {
  path?: string
  title: string
  action?: string
  subject?: string
  disabled?: boolean
  badgeContent?: string
  externalLink?: boolean
  openInNewTab?: boolean
  icon?: string | string[] | ReactNode
  badgeColor?: 'default' | 'primary' | 'secondary' | 'success' | 'error' | 'warning' | 'info'
}

// For Server Side Navigation Menu
type NavLink = {
  icon?: string
  path?: string
  title: string
  action?: string
  subject?: string
  disabled?: boolean
  badgeContent?: string
  externalLink?: boolean
  openInNewTab?: boolean
  badgeColor?: 'default' | 'primary' | 'secondary' | 'success' | 'error' | 'warning' | 'info'
}
```

Here is the example code:

<code-group>
<code-block title="TS" active>
```ts
import { VerticalNavItemsType } from 'src/@core/layouts/types'

const navigation = (): VerticalNavItemsType => {
  return [
    {
      badgeColor: 'error',
      badgeContent: 'New',
      title: 'Form Validation',
      path: '/forms/form-validation',
      icon: 'mdi:checkbox-marked-circle-outline'
    },
    {
      disabled: true,
      icon: 'mdi:eye-off-outline',
      title: 'Disabled Menu'
    },
    {
      icon: 'mdi:material-ui',
      title: 'MUI Docs',
      externalLink: true,
      openInNewTab: true,
      path: 'https://mui.com/material-ui/getting-started/usage/'
    }
  ]
}

export default navigation
```
</code-block>

<code-block title="JS">
```js
const navigation = () => {
  return [
    {
      badgeColor: 'error',
      badgeContent: 'New',
      title: 'Form Validation',
      path: '/forms/form-validation',
      icon: 'mdi:checkbox-marked-circle-outline'
    },
    {
      disabled: true,
      icon: 'mdi:eye-off-outline',
      title: 'Disabled Menu'
    },
    {
      icon: 'mdi:material-ui',
      title: 'MUI Docs',
      externalLink: true,
      openInNewTab: true,
      path: 'https://mui.com/material-ui/getting-started/usage/'
    }
  ]
}

export default navigation
```
</code-block>
</code-group>

Result:

<img alt='navigation-links' class='medium-zoom' :src="$withBase('/images/layouts/navigation-vertical-links.png')" />

## Horizontal Navigation Structure

::: danger Important!
So, you have decided to use the Horizontal Layout and will create Horizontal Navigation based on the below docs. Please note that on smaller screens, our layout is converted to Vertical and you will also need to create Vertical Navigation.

Please refer to the [Vertical Navigation Structure](/guide/layout/navigation-menu-structure.html#vertical-navigation-structure) guide as well.
:::

Following are the items that you can create for your horizontal navigation:

- [Navigation Group](#_1-navigation-group)
- [Navigation Link](#_2-navigation-link)

### 1. Navigation Group

It is used to group some navigation groups and/or navigation links that are opened in a tooltip. To create a navigation group, you need to add an object with the following structure:

```ts
// For Static Navigation Menu
type NavGroup = {
  title: string
  action?: string
  subject?: string
  badgeContent?: string
  children?: (NavGroup | NavLink)[]
  icon?: string | string[] | ReactNode
  badgeColor?: 'default' | 'primary' | 'secondary' | 'success' | 'error' | 'warning' | 'info'
}

// For Server Side Navigation Menu
type NavGroup = {
  icon?: string
  title: string
  action?: string
  subject?: string
  badgeContent?: string
  children?: (NavGroup | NavLink)[]
  badgeColor?: 'default' | 'primary' | 'secondary' | 'success' | 'error' | 'warning' | 'info'
}
```

Here is the example code:

<code-group>
<code-block title="TS" active>
```ts
import { HorizontalNavItemsType } from 'src/@core/layouts/types'

const navigation = (): HorizontalNavItemsType => {
  return [
    {
      title: 'UI',
      badgeContent: '3',
      badgeColor: 'warning',
      icon: 'mdi:palette-swatch-outline',
      children: [
        {
          title: 'Typography',
          icon: 'mdi:format-letter-case',
          path: '/ui/typography'
        },
        {
          title: 'Components',
          icon: 'mdi:archive-outline',
          children: [
            {
              title: 'Accordion',
              path: '/components/accordion'
            },
            {
              title: 'Alerts',
              path: '/components/alerts'
            }
          ]
        },
        {
          title: 'Icons',
          path: '/ui/icons',
          icon: 'mdi:google-circles-extended'
        }
      ]
    }
  ]
}

export default navigation
```
</code-block>

<code-block title="JS">
```js
const navigation = () => {
  return [
    {
      title: 'UI',
      badgeContent: '3',
      badgeColor: 'warning',
      icon: 'mdi:palette-swatch-outline',
      children: [
        {
          title: 'Typography',
          icon: 'mdi:format-letter-case',
          path: '/ui/typography'
        },
        {
          title: 'Components',
          icon: 'mdi:archive-outline',
          children: [
            {
              title: 'Accordion',
              path: '/components/accordion'
            },
            {
              title: 'Alerts',
              path: '/components/alerts'
            }
          ]
        },
        {
          title: 'Icons',
          path: '/ui/icons',
          icon: 'mdi:google-circles-extended'
        }
      ]
    }
  ]
}

export default navigation
```
</code-block>
</code-group>

Result:

<img alt='navigation-group' class='medium-zoom' :src="$withBase('/images/layouts/navigation-horizontal-group.png')" />

### 2. Navigation Link

To create a navigation link, you need to add an object with the following structure:

```ts
// For Static Navigation Menu
type NavLink = {
  path?: string
  title: string
  action?: string
  subject?: string
  disabled?: boolean
  badgeContent?: string
  externalLink?: boolean
  openInNewTab?: boolean
  icon?: string | string[] | ReactNode
  badgeColor?: 'default' | 'primary' | 'secondary' | 'success' | 'error' | 'warning' | 'info'
}

// For Server Side Navigation Menu
type NavLink = {
  icon?: string
  path?: string
  title: string
  action?: string
  subject?: string
  disabled?: boolean
  badgeContent?: string
  externalLink?: boolean
  openInNewTab?: boolean
  badgeColor?: 'default' | 'primary' | 'secondary' | 'success' | 'error' | 'warning' | 'info'
}
```

Here is the example code:

<code-group>
<code-block title="TS" active>
```ts
import { HorizontalNavItemsType } from 'src/@core/layouts/types'

const navigation = (): HorizontalNavItemsType => {
  return [
    {
      badgeColor: 'error',
      badgeContent: 'New',
      title: 'Form Validation',
      path: '/forms/form-validation',
      icon: 'mdi:checkbox-marked-circle-outline'
    },
    {
      disabled: true,
      icon: 'mdi:eye-off-outline',
      title: 'Disabled Menu'
    },
    {
      icon: 'mdi:material-ui',
      title: 'MUI Docs',
      externalLink: true,
      openInNewTab: true,
      path: 'https://mui.com/material-ui/getting-started/usage/'
    }
  ]
}

export default navigation
```
</code-block>

<code-block title="JS">
```js
const navigation = () => {
  return [
    {
      badgeColor: 'error',
      badgeContent: 'New',
      title: 'Form Validation',
      path: '/forms/form-validation',
      icon: 'mdi:checkbox-marked-circle-outline'
    },
    {
      disabled: true,
      icon: 'mdi:eye-off-outline',
      title: 'Disabled Menu'
    },
    {
      icon: 'mdi:material-ui',
      title: 'MUI Docs',
      externalLink: true,
      openInNewTab: true,
      path: 'https://mui.com/material-ui/getting-started/usage/'
    }
  ]
}

export default navigation
```
</code-block>
</code-group>

Result:

<img alt='navigation-links' class='medium-zoom' :src="$withBase('/images/layouts/navigation-horizontal-links.png')" />
