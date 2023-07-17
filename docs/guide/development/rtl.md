# RTL

## Change to RTL

We provide Left to Right (LTR) by default but you can easily change it to Right to Left (RTL).

To change the whole template to RTL, you need to go to the `src/configs/themeConfig.ts` file and change the `direction` property from `ltr` to `rtl`.

## RTL Toggler

You can also make a direction toggler which toggle between LTR and RTL directions. Look at the following code to make one:

<code-group>
<code-block title="TSX" active>
```tsx
import Switch from '@mui/material/Switch'
import { Direction } from '@mui/material'
import { useSettings } from 'src/@core/hooks/useSettings'
import FormControlLabel from '@mui/material/FormControlLabel'

const DirectionToggler = () => {
  const { settings, saveSettings } = useSettings()

  const handleDirectionChange = (value: Direction) => {
    saveSettings({ ...settings, direction: value })
  }

  return (
    <FormControlLabel
      label='RTL'
      control={
        <Switch
          checked={settings.direction === 'rtl'}
          onChange={e => handleDirectionChange(e.target.checked ? 'rtl' : 'ltr')}
        />
      }
    />
  )
}

export default DirectionToggler
```
</code-block>

<code-block title="JSX">
```jsx
import Switch from '@mui/material/Switch'
import { useSettings } from 'src/@core/hooks/useSettings'
import FormControlLabel from '@mui/material/FormControlLabel'

const DirectionToggler = () => {
  const { settings, saveSettings } = useSettings()

  const handleDirectionChange = value => {
    saveSettings({ ...settings, direction: value })
  }

  return (
    <FormControlLabel
      label='RTL'
      control={
        <Switch
          checked={settings.direction === 'rtl'}
          onChange={e => handleDirectionChange(e.target.checked ? 'rtl' : 'ltr')}
        />
      }
    />
  )
}

export default DirectionToggler
```
</code-block>
</code-group>

## Get current direction

You might need to render some code conditionally based on the current direction of the template. You can write the following code to do so:

```tsx{1,4,6}
import { useSettings } from 'src/@core/hooks/useSettings'

const SomeComponent = () => {
  const { settings } = useSettings()

  if (settings.direction === 'rtl') {
    return (
      {/* Some code */}
    )
  } else {
    return (
      {/* Some other code */}
    )
  }
}

export default SomeComponent
```

If you need to style something conditionally based on the current direction of the template, do the following:

```tsx{2,5,8}
import Box from '@mui/material/Box'
import { useSettings } from 'src/@core/hooks/useSettings'

const SomeComponent = () => {
  const { settings } = useSettings()

  return (
    <Box sx={{ backgroundColor: settings.direction === 'rtl' ? 'red' : 'blue' }}>
      ...
    </Box>
  )
}

export default SomeComponent
```

## Remove RTL from the template

To remove the RTL from the whole template, follow these steps:

- Remove all the plugins related to RTL. View all the dependencies of RTL in [this](/guide/overview/dependencies.html#right-to-left-rtl) section
- Replace the following code in the `src/layouts/components/Direction.tsx` file:

<code-group>
<code-block title="TSX" active>
```tsx{10}
import { ReactNode } from 'react'

interface DirectionProps {
  children: ReactNode
}

const Direction = (props: DirectionProps) => {
  const { children } = props

  return <>{children}</>
}

export default Direction
```
</code-block>

<code-block title="JSX">
```jsx{4}
const Direction = props => {
  const { children } = props

  return <>{children}</>
}

export default Direction
```
</code-block>
</code-group>
