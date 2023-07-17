# Override Components

You can override any components explained above in MUI and Custom sections.

Let us assume that you want to override the Page Header component.

You need to make a new file in the `src/layouts/components` folder. Copy the code from the `src/@core/components/page-header/index.tsx` file and paste it into the new file you just made. And then, you just need to write the component however you want.

<code-group>
<code-block title="TSX" active>
```tsx
// src/layouts/components/page-header/index.tsx

import Grid from '@mui/material/Grid'
import Typography from '@mui/material/Typography'

interface PageHeaderProps {
  title: string
  subtitle?: string
}

const UserPageHeader = ({ title, subtitle }: PageHeaderProps) => {
  return (
    <Grid item xs={12}>
      <Typography variant='h5'>{title}</Typography>
      {subtitle ? <Typography variant='caption'>{subtitle}</Typography> : null}
    </Grid>
  )
}

export default UserPageHeader
```
</code-block>

<code-block title="JSX">
```jsx
// src/layouts/components/page-header/index.js

import Grid from '@mui/material/Grid'
import Typography from '@mui/material/Typography'

const UserPageHeader = ({ title, subtitle }) => {
  return (
    <Grid item xs={12}>
      <Typography variant='h5'>{title}</Typography>
      {subtitle ? <Typography variant='caption'>{subtitle}</Typography> : null}
    </Grid>
  )
}

export default UserPageHeader
```
</code-block>
</code-group>

```tsx
// using `src/layouts/components/page-header` component in any of your pages

import UserPageHeader from 'src/layouts/components/page-header'

<UserPageHeader title='React ApexCharts' subtitle='React Component for ApexCharts' />
```
