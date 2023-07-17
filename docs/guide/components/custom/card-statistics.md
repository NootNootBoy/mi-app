# Card Statistics

## Overview

We have create different version of card components to make it easier for you to show your statistics neatly.

## Card Statistics Horizontal

```jsx
import Icon from 'src/@core/components/icon'
import CardStatisticsHorizontal from 'src/@core/components/card-statistics/card-stats-horizontal'

const Component = () => (
  <CardStatisticsHorizontal
    stats='58,352'
    trendNumber=29
    title='Sessions'
    subtitle='Last week analytics'
    icon={<Icon icon='bx:trending-up' />}
  />
)

export default Component
```

Result:

<img alt='card-stats-horizontal' class='medium-zoom' :src="$withBase('/images/components/card-stats-horizontal.png')" />

### Props

| Prop            | Type                                                          | Required | Description                                         |
| :-------------- | :------------------------------------------------------------ |:-------- | :-------------------------------------------------- |
| title           | `string`                                                      | Yes      | Title of the card                                   |
| stats           | `string`                                                      | Yes      | The statistic number on the card                    |
| subtitle        | `string`                                                      | Yes      | Subtitle of the card                                |
| avatarIcon      | `string`                                                      | Yes      | Icon inside the avatar                              |
| trendNumber     | `string`                                                      | Yes      | To show the difference in numbers                   |
| trend           | `positive`, `negative`                                        | No       | To show the change in numbers than previous numbers |
| avatarColor     | `primary`, `secondary`, `success`, `error`, `warning`, `info` | No       | Color of the avatar                                 |
| avatarIconProps | `Omit<IconProps, 'icon'>`                                     | No       | Props of the icon inside the avatar                 |

## Card Statistics Vertical

```jsx
import Icon from 'src/@core/components/icon'
import CardStatisticsVertical from 'src/@core/components/card-statistics/card-stats-vertical'

const Component = () => (
  <CardStatisticsVertical
    stats='$14,854'
    avatarSrc='...'
    trendNumber=28.14
    title='Transactions'
    optionsMenuProps={{ options: ['Refresh', 'Share', 'Update'] }}
  />
)

export default Component
```

Result:

<img alt='card-stats-vertical' class='medium-zoom' :src="$withBase('/images/components/card-stats-vertical.png')" />
<img alt='card-stats-vertical' class='medium-zoom' :src="$withBase('/images/components/card-stats-vertical-2.png')" />

### Props

| Prop             | Type                                                          | Required | Description                                         |
| :--------------- | :------------------------------------------------------------ |:-------- | :-------------------------------------------------- |
| title            | `string`                                                      | Yes      | Title of the card                                   |
| stats            | `string`                                                      | Yes      | The statistic number on the card                    |
| trendNumber      | `string`                                                      | Yes      | To show the difference in numbers                   |
| avatarIcon       | `string`                                                      | No       | Icon inside the avatar                              |
| avatarSrc        | `string`                                                      | No       | Path of the image                                   |
| trend            | `positive`, `negative`                                        | No       | To show the change in numbers than previous numbers |
| avatarColor      | `primary`, `secondary`, `success`, `error`, `warning`, `info` | No       | Color of the avatar                                 |
| avatarIconProps  | `Omit<IconProps, 'icon'>`                                     | No       | Props of the icon inside the avatar                 |
| optionsMenuProps | `OptionsMenuType`                                             | No       | Options to render in the more options menu          |

## Card Statistics With Target

```jsx
import CardStatisticsTarget from 'src/@core/components/card-statistics/card-stats-target'

const Component = () => (
  <CardStatisticsTarget
    stats='$1,271'
    trendNumber=23
    trend='negative'
    avatarColor='info'
    buttonText='Today'
    title='Referral Income'
    subtitle='34% of target'
    avatarIcon='bx:dollar'
    buttonOptions={['Yesterday', 'Last Week', 'Last Month']}
  />
)

export default Component
```

Result:

<img alt='card-stats-target' class='medium-zoom' :src="$withBase('/images/components/card-stats-target.png')" />
<img alt='card-stats-target-2' class='medium-zoom' :src="$withBase('/images/components/card-stats-target-2.png')" />

### Props

| Prop            | Type                                                          | Required | Description                                         |
| :-------------- | :------------------------------------------------------------ |:-------- | :-------------------------------------------------- |
| title           | `string`                                                      | Yes      | Title of the card                                   |
| stats           | `string`                                                      | Yes      | The statistic number on the card                    |
| subtitle        | `string`                                                      | Yes      | Subtitle of the card                                |
| buttonText      | `string`                                                      | Yes      | Text in the button                                  |
| avatarIcon      | `string`                                                      | Yes      | Icon inside the avatar                              |
| trendNumber     | `string`                                                      | Yes      | To show the difference in numbers                   |
| buttonOptions   | `string[]`                                                    | Yes      | Options to render below the button                  |
| avatarColor     | `primary`, `secondary`, `success`, `error`, `warning`, `info` | No       | Color of the avatar                                 |
| trend           | `positive`, `negative`                                        | No       | To show the change in numbers than previous numbers |
| avatarIconProps | `Omit<IconProps, 'icon'>`                                     | No       | Props of the icon inside the avatar                 |
