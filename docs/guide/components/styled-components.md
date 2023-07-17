# Styled Components

## Overview

These are the styles available in the `src/@core/styles` folder:

- MUI Stepper
- Fullcalendar
- Keen Slider
- React Apexcharts
- CleaveJs
- React Credit Cards
- React Datepicker
- React Draft Wysiwyg
- React Dropzone
- React Hot Toast
- Recharts

::: tip
If you do not want to use these styles, then render your component directly. This will apply the default styles provided by MUI and/or third-party plugins.
:::

## Usage

You need to import styles as a component and wrap them around your components.

Let us take an example of React Datepicker:

```tsx
import DatePicker from 'react-datepicker'
import DatePickerWrapper from 'src/@core/styles/libs/react-datepicker'

<DatePickerWrapper>
  <DatePicker
    {...} // all of your props
  />
</DatePickerWrapper>
```

If you do not want to use these styles:

```tsx
import DatePicker from 'react-datepicker'

<DatePicker
  {...} // all of your props
/>
```

::: tip
If you have to use any styles with multiple components like multiple CleaveJS components used in a single page, then you need to import the styles once and then wrap the index file of that page with the styled component, so that the styles are not called multiple times.
:::

## Override Styled Components

Overriding these styles components is very easy. Follow these steps to override any styles:

- Make a new file in the `src/layouts/styles` folder
- Copy the code of that component that you want to override from the `src/@core/styles` folder and paste it into the new file that you just made
- Override the styles as per your project requirements

Let us say that you want to override the styles of React Credit Cards:

```ts
// src/layouts/styles/react-credit-cards/index.ts

import { styled } from '@mui/material/styles'

const CardWrapper = styled('div')(({ theme }) => ({
  display: 'flex',
  '& .rccs, & .rccs__card': {
    margin: theme.spacing(4)
  }
}))

export default CardWrapper
```

## React Hot Toast

The styles of React Hot Toast are globally included in the `src/pages/_app.tsx` file, so you do not need to add a wrapper in any of your toast components.

### Usage

```tsx
// src/pages/_app.tsx

import { Toaster } from 'react-hot-toast'
import ReactHotToast from 'src/@core/styles/libs/react-hot-toast'

<ReactHotToast>
  <Toaster position={settings.toastPosition} toastOptions={{ className: 'react-hot-toast' }} />
</ReactHotToast>
```

```tsx
import toast from 'react-hot-toast'

<button onClick={() => toast('Blank Toast')}>Open Toast</button>
```

### Override

To override the styles, you need to follow the same steps that are explained above. Now, suppose you want to open the toasts at their default position, then:

- Make a new file in the `src/layouts/styles` folder (say `src/layouts/styles/react-hot-toast/index.ts`)
- Copy the code from the `src/@core/styles/react-hot-toast/index.ts` file and paste it into the `src/layouts/styles/react-hot-toast/index.ts` file
- Remove the following code:

```ts
'& > div': {
  top: '75px !important',
  right: `${theme.spacing(6)} !important`
}
```

- Import and render `src/layouts/styles/react-hot-toast/index.ts` file in `src/pages/_app.tsx` file

```tsx
// src/pages/_app.tsx

import { Toaster } from 'react-hot-toast'
import UserReactHotToast from 'src/layouts/styles/react-hot-toast'

<UserReactHotToast>
  <Toaster position={settings.toastPosition} toastOptions={{ className: 'react-hot-toast' }} />
</UserReactHotToast>
```

```tsx
import toast from 'react-hot-toast'

<button onClick={() => toast('Blank Toast')}>Open Toast</button>
```
