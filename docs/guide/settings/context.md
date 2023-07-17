# Settings Context

## Overview

Settings Context has been created so that the template is independent of the redux store for storing the variables used in the template.

## Properties

Following are the properties and their values that are stored in the Settings Context:

| Properties            | Values                             | Description                                                           |
| :-------------------- | :--------------------------------- | :-------------------------------------------------------------------- |
| skin                  | `default`, `bordered`              | Change template skin                                                  |
| mode                  | `light`, `dark`, `semi-dark`       | Set Light or Dark mode for the template                               |
| direction             | `ltr`, `rtl`                       | Content direction                                                     |
| navCollapsed          | `true`, `false`                    | If `true`, the vertical navigation menu is collapsed                  |
| navHidden             | `true`, `false`                    | If `true`, the navigation menu is hidden                              |
| layout                | `vertical`, `horizontal`           | Set Vertical or Horizontal layout for the template                    |
| lastLayout            | `vertical`, `horizontal`           | For internal usage (used when window is resized in Horizontal layout) |
| verticalNavToggleType | `accordion`, `collapse`            | Set behavior of menu group in the vertical navigation menu            |
| contentWidth          | `full`, `boxed`                    | Full or container width of AppBar, Content and Footer                 |
| appBar                | `fixed`, `static`, `hidden`        | Change appBar position                                                |
| appBarBlur            | `true`, `false`                    | If `true`, appBar will appear with opacity                            |
| footer                | `fixed`, `static`, `hidden`        | Change footer position                                                |
| themeColor            | `primary`, `secondary`, `success`, `error`, `warning`, `info` | Change primary color in the template       |
| toastPosition         | `top-left`, `top-center`, `top-right`, `bottom-left`, `bottom-center`, `bottom-right` | Default toast position of `react-hot-toast` |

## LocalStorage

Following are the properties and their values that are stored in `localStorage` from the Settings Context:

| Properties            | Values                                                        | Description                                                |
| :-------------------- | :------------------------------------------------------------ | :--------------------------------------------------------- |
| skin                  | `default`, `bordered`                                         | Change template skin                                       |
| mode                  | `light`, `dark`, `semi-dark`                                  | Set Light or Dark mode for the template                    |
| direction             | `ltr`, `rtl`                                                  | Content direction                                          |
| navCollapsed          | `true`, `false`                                               | If `true`, the vertical navigation menu is collapsed       |
| verticalNavToggleType | `accordion`, `collapse`                                       | Set behavior of menu group in the vertical navigation menu |
| contentWidth          | `full`, `boxed`                                               | Full or container width of AppBar, Content and Footer      |
| appBarBlur            | `true`, `false`                                               | If `true`, appBar will appear with opacity                 |
| themeColor            | `primary`, `secondary`, `success`, `error`, `warning`, `info` | Change primary color in the template                       |

## Provider and Consumer

Settings context relies on the [context feature of React](https://reactjs.org/docs/context.html) to pass the settings down to the components. Settings context exports `SettingsProvider` and `SettingsConsumer` and they must be parents of `ThemeComponent` in `src/pages/_app.tsx` file. See the following code:

```tsx
<SettingsProvider>
  <SettingsConsumer>
    {({ settings }) => (
      <ThemeComponent settings={settings}>{getLayout(<Component {...pageProps} />)}</ThemeComponent>
    )}
  </SettingsConsumer>
</SettingsProvider>
```
