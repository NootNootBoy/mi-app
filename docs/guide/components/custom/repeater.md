# Repeater

## Overview

We have created a Repeater component to duplicate a component.

## Usage

```tsx{4,12-14}
import { useState } from 'react'
import Button from '@mui/material/Button'
import Typography from '@mui/material/Typography'
import Repeater from 'src/@core/components/repeater'

const Component = () => {
  const [count, setCount] = useState(1)

  return (
    <>
      <Button onClick={() => setCount(count + 1)}>Add 1</Button>
      <Repeater count={count}>
        {i => <Typography key={i}>{`Count = ${i + 1}`}</Typography>}
      </Repeater>
    </>
  )
}

export default Component
```

## Props

| Prop       | Type                     | Required | Description                                           |
| :--------- | :----------------------- | :------- | :---------------------------------------------------- |
| count      | `number`                 | Yes      | Number of times that the component should be repeated |
| tag        | `React.ComponentType`    | No       | Component Tag                                         |
| children   | `(i: number): ReactNode` | Yes      | Your content that you want to repeat                  |
