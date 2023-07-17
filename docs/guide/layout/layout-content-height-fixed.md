# Layout Content with Fixed Height

## Overview

You can use this layout if you want a fixed height of the content area. For example, apps like Email and Chat need a fixed height and a scrollbar should be inside these apps.

::: danger Heads Up!
Do not remove any code related to `contentHeightFixed` from the `src/layouts/UserLayout.tsx` file. Otherwise, the whole template would break.
:::

## Usage

You need to use the `contentHeightFixed` method on your component to fix the height of the content area.

The type accepted by this method is:

```ts
contentHeightFixed?: boolean
```

Here is the example code:

```tsx
const Component = () => {
  return (
    // your content
  )
}

Component.contentHeightFixed = true

export default Component
```
