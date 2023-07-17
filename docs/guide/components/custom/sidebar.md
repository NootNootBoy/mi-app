# Sidebar

## Overview

We have created a sidebar component with position `absolute` in case you need to show a sidebar inside a container. You can see this component used in Email and Chat apps.

## Usage

```tsx{2,9}
import { useEffect } from 'react'
import Sidebar from 'src/@core/components/sidebar'

const Component = () => {
  const [show, setShow] = useState(false)

  return (
    <>
      <Sidebar show={show}>{children}</Sidebar>
      {/* Your some content */}
    </>
  )
}

export default Component
```

## Props

| Prop          | Type            | Required | Description                                    |
| :------------ | :-------------- | :------- | :--------------------------------------------- |
| show          | `true`, `false` | Yes      | If `true`, sidebar is visible                  |
| hideBackdrop  | `true`, `false` | No       | If `true`, sidebar backdrop is hidden          |
| direction     | `left`, `right` | No       | If `left`, open sidebar from the left side     |
| onOpen        | `function`      | No       | Callback function on open of sidebar           |
| onClose       | `function`      | No       | Callback function on close of sidebar          |
| backDropClick | `function`      | No       | Callback function on click of sidebar backdrop |
