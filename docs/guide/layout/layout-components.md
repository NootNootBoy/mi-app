---
sidebarDepth: 2
---

# Layout Components

## Overview

On this page, you'll get to know how the layout components are rendered so that it would be easy for you to override these layout components.

## Vertical Layout Components

Vertical Layout is formed with the following layout components. Let's understand each one of them:

### 1. Navigation Menu (left sidebar)

The navigation menu is created with the following components:

- Navigation Header which uses the `VerticalNavHeader` component

  <img alt='vertical-menu-header' class='medium-zoom' :src="$withBase('/images/layouts/vertical-menu-header.png')" />

- `VerticalNavItems` component is used to categorize whether an item is a section header, navigation group or navigation link
- Navigation Section Header which uses the `VerticalNavSectionTitle` component

  <img alt='vertical-menu-section-header' class='medium-zoom' :src="$withBase('/images/layouts/vertical-menu-section-header.png')" />

- Navigation Group which uses the `VerticalNavGroup` component

  <img alt='vertical-menu-group' class='medium-zoom' :src="$withBase('/images/layouts/vertical-menu-group.png')" />

- Navigation Link which uses the `VerticalNavLink` component

  <img alt='vertical-menu-link' class='medium-zoom' :src="$withBase('/images/layouts/vertical-menu-link.png')" />

### 2. Navbar (or AppBar)

AppBar is created with the following components:

#### Left side section

- Template Search which uses the `Autocomplete` component

#### Right side section

- Change language by using the `LanguageDropdown` component
- Light and Dark Mode Toggler which uses the `ModeToggler` component
- Notifications of the User which uses the `NotificationDropdown` component
- User Actions which uses the `UserDropdown` component

### 3. Footer

Footer is created with the following components:

1. Copyright on the left side
2. Important links of the company on the right side

## Horizontal Layout Components

Horizontal Layout is formed with the following layout components. Let's understand each one of them:

### 1. Navbar (or AppBar)

AppBar is created with the following components:

#### Left side section

- Company Logo and/or Company Name

#### Right side section

- Template Search which uses the `Autocomplete` component
- Change language by using the `LanguageDropdown` component
- Light and Dark Mode Toggler which uses the `ModeToggler` component
- Notifications of the User which uses the `NotificationDropdown` component
- User Actions which uses the `UserDropdown` component

### 2. Navigation Menu

The navigation menu is created with the following components:

- `HorizontalNavItems` component is used to categorize whether an item is a navigation group or navigation link
- Navigation Group which uses the `HorizontalNavGroup` component

  <img width='500' class='medium-zoom' alt='horizontal-menu-group' :src="$withBase('/images/layouts/horizontal-menu-group.png')" />

- Navigation Link which uses the `HorizontalNavLink` component

  <img width='500' class='medium-zoom' alt='horizontal-menu-link' :src="$withBase('/images/layouts/horizontal-menu-link.png')" />

### 3. Footer

Footer is created with the following components:

- Copyright on left side
- Important links of the company on the right side

## Blank Layout with AppBar Component

Blank Layout with AppBar provides only appBar (at top of the page) which contains the Company logo and Company name only.

## Scroll to top Component

Fab button is created at the bottom-right side of a page to scroll to the top of the page. It is available only in Vertical and Horizontal layouts. It is not visible at top of the page. It is only visible when the page is scrolled more than 400px.

<img alt='scroll-to-top' class='medium-zoom' :src="$withBase('/images/layouts/scroll-to-top.png')" />
