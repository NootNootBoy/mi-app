# Page Header

## Overview

We have created a component to easily add a page title and subtitle to any of your pages. By using this, all of your page headers will be uniform.

::: danger Heads Up!
You need to render this component as a direct child of MUI's `<Grid container>` component.
:::

## Usage

```tsx{4,9-20}
import Grid from '@mui/material/Grid'
import Link from '@mui/material/Link'
import Typography from '@mui/material/Typography'
import PageHeader from 'src/@core/components/page-header'

const Component = () => {
  return (
    <Grid container spacing={6}>
      <PageHeader
        title={
          <Typography variant='h5'>
            <Link href='https://github.com/facebook/react' target='_blank'>React</Link>
          </Typography>
        }
        subtitle={
          <Typography variant='body2'>
            A declarative, efficient, and flexible JavaScript library for building user interfaces.
          </Typography>
        }
      />
    </Grid>
  )
}

export default Component
```

## Props

| Prop      | Type        | Required | Description                    |
| :-------- | :---------- | :------- | :----------------------------- |
| title     | `ReactNode` | Yes      | Title of the page goes here    |
| subtitle  | `ReactNode` | No       | Subtitle of the page goes here |
