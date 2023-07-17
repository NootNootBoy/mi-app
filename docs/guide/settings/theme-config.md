# Theme Configurations

## Overview

To configure your template, we will be using the `src/configs/themeConfig.ts` file, which has all the template configurations listed with their valid values. Just change the configurations as per your requirement and you are done.

If you are looking to match up with one of our demos, then please read [demo configs](/guide/development/demo-config.html) doc.

::: danger Important
Make sure you clear the browser's local storage in order to see the config changes in the template. Refer: <strong>[How to clear local storage?](https://www.leadshook.com/help/how-to-clear-local-storage-in-google-chrome-browser/)</strong>
:::

## Properties

Following are the properties with their values that we have used in the theme:

<code-group>
<code-block title="TS" active>
```ts
const themeConfig: ThemeConfig = {
  templateName: 'Sneat',
  layout: 'vertical',
  mode: 'light',
  direction: 'ltr',
  skin: 'default',
  contentWidth: 'boxed',
  footer: 'static',
  routingLoader: true,
  navHidden: false,
  menuTextTruncate: true,
  navSubItemIcon: 'mdi:circle-outline',
  verticalNavToggleType: 'accordion',
  navCollapsed: false,
  navigationSize: 260,
  collapsedNavigationSize: 69,
  afterVerticalNavMenuContentPosition: 'fixed',
  beforeVerticalNavMenuContentPosition: 'fixed',
  horizontalMenuToggle: 'hover',
  horizontalMenuAnimation: true,
  appBar: 'fixed',
  appBarBlur: true,
  responsiveFontSizes: true,
  disableRipple: false,
  disableCustomizer: false,
  toastPosition: 'top-right'
}
```
</code-block>

<code-block title="JS">
```js
const themeConfig = {
  templateName: 'Sneat',
  layout: 'vertical',
  mode: 'light',
  direction: 'ltr',
  skin: 'default',
  contentWidth: 'boxed',
  footer: 'static',
  routingLoader: true,
  navHidden: false,
  menuTextTruncate: true,
  navSubItemIcon: 'mdi:circle-outline',
  verticalNavToggleType: 'accordion',
  navCollapsed: false,
  navigationSize: 260,
  collapsedNavigationSize: 69,
  afterVerticalNavMenuContentPosition: 'fixed',
  beforeVerticalNavMenuContentPosition: 'fixed',
  horizontalMenuToggle: 'hover',
  horizontalMenuAnimation: true,
  appBar: 'fixed',
  appBarBlur: true,
  responsiveFontSizes: true,
  disableRipple: false,
  disableCustomizer: false,
  toastPosition: 'top-right'
}
```
</code-block>
</code-group>

### beforeVerticalNavMenuContentPosition

If the value is set to `static`, then the content will get scrolled along with the vertical navigation. If the value is set to `fixed`, then the content will not get scrolled along with the vertical navigation.

#### beforeVerticalNavMenuContentPosition: 'static'

<br />
<img class='medium-zoom' alt='add-static-content-before-menu-items' :src="$withBase('/images/settings/static-before-content.png')" />

#### beforeVerticalNavMenuContentPosition: 'fixed'

<br />
<img class='medium-zoom' alt='add-fixed-content-before-menu-items' :src="$withBase('/images/settings/fixed-before-content.png')" />

### afterVerticalNavMenuContentPosition

If the value is set to `static`, then the content will get scrolled along with the vertical navigation. If the value is set to `fixed`, then the content will not get scrolled along with the vertical navigation.

#### afterVerticalNavMenuContentPosition: 'static'

<br />
<img class='medium-zoom' alt='add-static-content-after-menu-items' :src="$withBase('/images/settings/static-after-content.png')" />

#### afterVerticalNavMenuContentPosition: 'fixed'

<br />
<img class='medium-zoom' alt='add-fixed-content-after-menu-items' :src="$withBase('/images/settings/fixed-after-content.png')" />

## Property Options

Following is the table of all the properties and their possible values that are available in the theme configurations:

| Properties                           | Values                             | Description                                                                 |
| :----------------------------------- | :--------------------------------- | :-------------------------------------------------------------------------- |
| templateName                         | `string`                           | Name of the template, project or company                                    |
| layout                               | `vertical`, `horizontal`           | Set Vertical or Horizontal layout for the template                          |
| mode                                 | `light`, `dark`, `semi-dark`       | Set Light or Dark mode for the template                                     |
| direction                            | `ltr`, `rtl`                       | Content direction                                                           |
| skin                                 | `default`, `bordered`              | Change template skin                                                        |
| contentWidth                         | `full`, `boxed`                    | Full or container width of AppBar, Content and Footer                       |
| footer                               | `fixed`, `static`, `hidden`        | Change footer position                                                      |
| routingLoader                        | `true`, `false`                    | Loader on top of the app on route change                                    |
| navHidden                            | `true`, `false`                    | If `true`, the navigation menu is hidden                                    |
| menuTextTruncate                     | `true`, `false`                    | If `true`, text truncate in the navigation menu is enabled                  |
| navSubItemIcon                       | `string`                           | Change icon for the sub menus in the navigation menu                        |
| verticalNavToggleType                | `accordion`, `collapse`            | Set behavior of menu group in the vertical navigation menu                  |
| navCollapsed                         | `true`, `false`                    | If `true`, the vertical navigation menu is collapsed                        |
| navigationSize                       | `number`                           | Width of navigation menu when menu is not collapsed                         |
| collapsedNavigationSize              | `number`                           | Width of navigation menu when menu is collapsed                             |
| afterVerticalNavMenuContentPosition  | `fixed`, `static`                  | Position of the content which is added after the vertical navigation menu   |
| beforeVerticalNavMenuContentPosition | `fixed`, `static`                  | Position of the content which is added before the vertical navigation menu  |
| horizontalMenuToggle                 | `click`, `hover`                   | Set behavior of menu group in the horizontal navigation menu                |
| horizontalMenuAnimation              | `true`, `false`                    | If `true`, animation is enabled for the horizontal navigation menu          |
| appBar                               | `fixed`, `static`, `hidden`        | Change appBar position                                                      |
| appBarBlur                           | `true`, `false`                    | If `true`, background of appBar will have opacity                           |
| responsiveFontSizes                  | `true`, `false`                    | If `true`, responsive font sizes are enabled                                |
| disableRipple                        | `true`, `false`                    | If `true`, the Ripple effect is disabled                                    |
| disableCustomizer                    | `true`, `false`                    | If `true`, customizer is disabled as right sidebar to configure in live app |
| toastPosition                        | `top-left`, `top-center`, `top-right`, `bottom-left`, `bottom-center`, `bottom-right` | Set default toast position in the template |
