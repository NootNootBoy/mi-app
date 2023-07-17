# Layout Types

::: tip
We recommend you to go through the [Layout Docs of NextJS](https://nextjs.org/docs/basic-features/layouts) to understand how the layout works in the app. Once you understand the layout from NextJS, then you may go through our docs for a better understanding.
:::

## Overview

We provide four types of layouts:

- [Vertical Layout](#vertical-layout),
- [Horizontal Layout](#horizontal-layout),
- [Blank Layout](#blank-layout) and
- [Blank Layout with AppBar](#blank-layout-with-appbar).

Each of them is explained in detail.

## Vertical Layout

This is the default layout. With this layout, you will get the following layout components:

- Navigation Menu (left sidebar)
- Navbar (at top of the page)
- Footer (at bottom of the page)

Each layout component are explained [here](/guide/layout/layout-components.html#vertical-layout-components).

All of the above layout components are configurable. You can customize any or all layout components using [themeConfig](/guide/settings/theme-config.html) to get your desired layout.

Vertical Layout looks like this:

<img class='medium-zoom' alt='vertical-layout-preview' :src="$withBase('/images/layouts/vertical-layout.png')" />

## Horizontal Layout

You can make this your default layout. With this layout, you will get the following layout components:

- Navbar (at top of the page)
- Navigation Menu (on top of the page below the Navbar)
- Footer (at bottom of the page)

Each layout component are explained [here](/guide/layout/layout-components.html#horizontal-layout-components).

All of the above layout components are configurable. You can customize any or all layout components using [themeConfig](/guide/settings/theme-config.html) to get your desired layout.

Horizontal Layout looks like this:

<img alt='horizontal-layout-preview' class='medium-zoom' :src="$withBase('/images/layouts/horizontal-layout.png')" />

## Blank Layout

This is useful if you want to create pages without any other content and where you don't need a navbar, navigation menu and footer. For example, an _Authentication_ page.

This is a blank page where you can create everything from scratch.

Blank Layout in _Login_ page looks like this:

<img alt='blank-layout-login-preview' class='medium-zoom' :src="$withBase('/images/layouts/blank-layout-login.png')" />

## Blank Layout with AppBar

This is useful if you want to create pages where you don't need a navigation menu and footer. For example, an _Authentication_ page. With this layout, you will get a navbar (or AppBar) on top of the page.

AppBar is explained [here](/guide/layout/layout-components.html#blank-layout-with-appbar-component).

Blank Layout with AppBar in _Login_ page looks like this:

<img alt='blank-layout-with-appBar-login-preview' class='medium-zoom' :src="$withBase('/images/layouts/blank-layout-with-appBar-login.png')" />
