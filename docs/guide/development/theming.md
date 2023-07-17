# Theming

## Overview

Theming is the most important aspect of any template. You can easily customize theme of our template. You can change the colors, the typography, the spacing and much more.

MUI offers a utility function: createTheme() that creates a theme which can be passed to the theme provider; otherwise the theme provider uses the default theme. The theme provider makes the theme available in the component tree, and can be used via the sx prop, or inside styled components using the MUI styled engine (styled).

::: danger Important
Make your changes in `src/layouts/UserThemeOptions.ts` file in order to override colors, typography, spacing or any other component styling. Do not make any changes related to theme inside of @core folder unless suggested by our support team.

Consider reading [MUI theming docs](https://mui.com/material-ui/customization/theming/) to understand how it works and how to access and override theme.
:::

- [How to override Color Palette](#how-to-override-color-palette)
- [How to customize MUI component appearance](#how-to-customize-mui-component-appearance)
- [How to override Typography](#how-to-override-typography)
- [How to override Shadows](#how-to-override-shadows)
- [How to override Breakpoints](#how-to-override-breakpoints)
- [How to override components styling](#how-to-override-components-styling)

## How to override Color Palette

### How to Change Colors

In order to change primary color, open `src/layouts/UserThemeOptions.ts` file and uncomment the palette object returned from that file.

```ts
palette:{
  primary: {
    light: '#8082FF',
    main: '#696CFF',
    dark: '#6062E8',
    contrastText: '#FFF'
  },
  secondary: {
    ...
  },
  success: {
    ...
  },
  error: {
    ...
  },
  warning: {
    ...
  },
  info: {
    ...
  }
}
```

Colors given in the above palette object are current primary colors used in our template, update those colors according to your project requirements.

Above example shows how to change primary colors. You can change any colors of the palette in the same way shown above. Please refer [how to customize MUI palette documentation](https://mui.com/material-ui/customization/palette/). Also refer our core palette from the file `src/@core/theme/palette/index.ts` in order to check custom colors, dark / light colors etc.. for better idea.

### Colors Tool

Eva color tool [https://colors.eva.design/](https://colors.eva.design/)

We recommend picking colors with these values:

- light : 400
- main : 500
- dark : 600
- contrastText: '#FFF'

<img height="500" alt='color-tool' class='medium-zoom' :src="$withBase('/images/development/color-palette.png')" />

## How to customize MUI component appearance

You can easily customize the appearance of any component, but it is important to understand how to customize it right way which will save the time, resources and provide optimum performance.

Please read MUI doc on how to [customize component appearance](https://mui.com/material-ui/customization/how-to-customize/) to get clear idea.

## How to override Typography

### How to change font

We have used [Inter fonts](https://fonts.google.com/specimen/Inter?query=inter) in the whole template. Now suppose you want to implement [Montserrat fonts](https://fonts.google.com/specimen/Montserrat?query=montserrat).

First open `src/pages/_document.tsx` file and change font's URL like following:

```tsx
<Head>
  ...
  <link
    rel='stylesheet'
    href='https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,300;0,400;0,500;0,600;1,400&display=swap'
  />
  ...
</Head>
```

Now, open `src/layouts/UserThemeOptions.ts` file and uncomment typography object like following:

```ts
typography: {
  fontFamily:
    '"Montserrat", sans-serif'
}
```

### Use multiple fonts

```ts
typography: {
  fontFamily:
    '"Inter", sans-serif',
  h1: {
    fontFamily:
    '"Montserrat", sans-serif',
    fontWeight: 700,
    fontSize: '3.5rem',
    lineHeight: 1.375
  },
}
```

::: tip Reference:
[https://demos.themeselection.com/sneat-mui-react-nextjs-admin-template/demo-1/ui/typography/](https://demos.themeselection.com/sneat-mui-react-nextjs-admin-template/demo-1/ui/typography/)

MUI: [https://mui.com/material-ui/customization/typography/](https://mui.com/material-ui/customization/typography/)
:::

## How to override Shadows

If you want to customize shadows, uncomment following from the `src/layouts/UserThemeOptions.ts` file and change shadows  according to your project requirement.

Make sure to enable mode from the settings which are already commented at the starting of this file if you are using dark / light both the versions. If you are using either of them, just override shadows without any conditions.

```ts
// Uncomment this if using light & dark both
const { mode } = settings
```

```ts
// conditional shadows for both dark / light
shadows: mode === 'light' ? [...] : [...]

// Only shadows if using only one from light / dark
shadows: [...]
```

## How to override Breakpoints

If you want to customize breakpoints, uncomment following from the `src/layouts/UserThemeOptions.ts` file and change breakpoints size according to your project requirement.

```ts
breakpoints: {
  values: {
    xs: 0,
    sm: 768,
    md: 992,
    lg: 1200,
    xl: 1920
  }
}
```

::: tip Reference:
[https://mui.com/material-ui/customization/breakpoints/](https://mui.com/material-ui/customization/breakpoints/)
:::

## How to override components styling

The theme's components key allows you to customize a component without wrapping it in another component. You can change the styles, the default props, and more.

Open `src/layouts/UserThemeOptions.ts` file and uncomment typography object like following:

``` ts
components: {
  MuiButton: {
    defaultProps: {
      disableElevation: true
    },
    ...
  },
  ...
}
```

::: tip Reference:
[https://mui.com/material-ui/customization/theme-components/](https://mui.com/material-ui/customization/theme-components/)
:::
