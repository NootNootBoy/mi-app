# Timeline Dot

## Overview

Please visit [MUI Timeline Docs](https://mui.com/material-ui/react-timeline/) for a proper explanation of the `TimelineDot` component.

TimelineDot component is slightly modified to make it more beautiful and useable. Let's have a glance.

::: tip Note
We have only mentioned the extended props here but you can still use the default MUI TimelineDot props.
:::

## Timeline Dot Skins

There is only one skin type of timeline dot: `light`.

Here is an example of how to use the skin:

```tsx
import Icon from 'src/@core/components/icon'
import CustomTimelineDot from 'src/@core/components/mui/timeline-dot'

<CustomTimelineDot skin='light' color='error'>
  <Icon icon='mdi:airplane' fontSize={20} />
</CustomTimelineDot>
<CustomTimelineDot skin='light' color='primary'>
  <Icon icon='mdi:clock-outline' fontSize={20} />
</CustomTimelineDot>
<CustomTimelineDot skin='light' color='warning'>
  <Icon icon='mdi:cart-outline' fontSize={20} />
</CustomTimelineDot>
<CustomTimelineDot skin='light' color='success'>
  <Icon icon='mdi:file-edit-outline' fontSize={20} />
</CustomTimelineDot>
```

Result:

<img alt='timeline-dot-skins' class='medium-zoom' :src="$withBase('/images/components/timeline-dot-skin.png')" />

## Props

| Prop | Type    | Required | Description              |
| :--- | :------ | :------- | :----------------------- |
| skin | `light` | No       | Skin of the timeline dot |
