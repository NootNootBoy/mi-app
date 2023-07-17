# Avatar

## Overview

Please visit [MUI Avatar Docs](https://mui.com/material-ui/react-avatar/) for a proper explanation of the `Avatar` component.

Avatar component is slightly modified to make it more beautiful and useable. Let's have a glance.

::: tip Note
We have only mentioned the extended props here but you can still use the default MUI avatar props.
:::

## Avatar Colors

Use the `color` prop so you don't have to use the `sx` prop and write the styles inside it.

Use the MUI colors `primary` | `secondary` | `success` | `error` | `warning` | `info` to create colored avatars.

Here is the example of how to use the colors mentioned above:

```tsx
import Icon from 'src/@core/components/icon'
import CustomAvatar from 'src/@core/components/mui/avatar'

<CustomAvatar color='primary'>
  <Icon icon='bx-bell' />
</CustomAvatar>
<CustomAvatar color='secondary'>
  <Icon icon='bx-bell' />
</CustomAvatar>
<CustomAvatar color='success'>
  <Icon icon='bx-bell' />
</CustomAvatar>
<CustomAvatar color='error'>
  <Icon icon='bx-bell' />
</CustomAvatar>
<CustomAvatar color='warning'>
  <Icon icon='bx-bell' />
</CustomAvatar>
<CustomAvatar color='info'>
  <Icon icon='bx-bell' />
</CustomAvatar>
```

Result:

<img alt='avatar-colors' class='medium-zoom' :src="$withBase('/images/components/avatar-colors.png')" />

## Avatar Skins

There are three skins avatar skins `filled` | `light` | `light-static`.

**Please Note:** The difference between `light` & `light-static` can only be seen in the **Dark layout**.

Here is the example of how to use the skins mentioned above:

```tsx
import CustomAvatar from 'src/@core/components/mui/avatar'

<CustomAvatar skin='filled'>N</CustomAvatar> // OR <CustomAvatar>N</CustomAvatar>
<CustomAvatar skin='light' color='error'>OP</CustomAvatar>
<CustomAvatar skin='light-static' color='error'>AB</CustomAvatar>
```

Result:

<img alt='avatar-skins' class='medium-zoom' :src="$withBase('/images/components/avatar-skins.png')" />

## Props

| Prop  | Type                                                          | Default   | Required | Description                    |
| :---- | :------------------------------------------------------------ | :-------- | :------- | :----------------------------- |
| skin  | `filled`, `light`, `light-static`                             | `filled`  | No       | Skin of the avatar             |
| color | `primary`, `secondary`, `success`, `error`, `warning`, `info` | `primary` | No       | Background color of the avatar |
