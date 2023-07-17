# Chip

## Overview

Please visit [MUI Chip Docs](https://mui.com/material-ui/react-chip/) for a proper explanation of the `Chip` component.

Chip component is slightly modified to make it more beautiful and useable. Let's have a glance.

::: tip Note
We have only mentioned the extended props here but you can still use the default MUI chip props.
:::

## Chip Skins

There is only one chip skin `light`.

Here is an example of how to use the skin:

```tsx
import CustomChip from 'src/@core/components/mui/chip'

<CustomChip label='Primary' skin='light' color='primary' />
<CustomChip label='Secondary' skin='light' color='secondary' />
<CustomChip label='Success' skin='light' color='success' />
<CustomChip label='Error' skin='light' color='error' />
<CustomChip label='Warning' skin='light' color='warning' />
<CustomChip label='Info' skin='light' color='info' />
```

Result:

<img alt='chips-skins' class='medium-zoom' :src="$withBase('/images/components/chips-skin.png')" />

## Chip Rounded

There is only one chip skin `light`.

Here is an example of how to use the skin:

```tsx
import CustomChip from 'src/@core/components/mui/chip'

<CustomChip rounded label='Primary' skin='light' color='primary' />
<CustomChip rounded label='Secondary' skin='light' color='secondary' />
<CustomChip rounded label='Success' skin='light' color='success' />
<CustomChip rounded label='Error' skin='light' color='error' />
<CustomChip rounded label='Warning' skin='light' color='warning' />
<CustomChip rounded label='Info' skin='light' color='info' />
```

Result:

<img alt='chips-rounded' class='medium-zoom' :src="$withBase('/images/components/chips-rounded.png')" />

## Props

| Prop    | Type      | Required | Description       |
| :---    | :------   | :------- | :---------------  |
| skin    | `light`   | No       | Skin of the chip  |
| rounded | `boolean` | No       | Shape of the chip |
