# Redux

Sneat uses [redux-toolkit](https://redux-toolkit.js.org/introduction/getting-started) for state-management.

## Overview

Sneat uses `redux-toolkit` with hooks to manage the state for the applications.

## Usage

You can find all of the slices in `src/store` folder and

You should read the [redux-toolkit](https://redux-toolkit.js.org/introduction/getting-started) documentation to better understand the template.

## Creating a slice

Create a new file in `src/store`, and name it `email.ts` and import `createSlice` from `@reduxjs/toolkit` package to create the new slice.

```ts
import { createSlice } from '@reduxjs/toolkit'

const initialState = {
  selectedMails: []
}

const emailSlice = createSlice({
  name: 'email',
  initialState,
  reducers: {}
})

export default appEmailSlice.reducer
```

## Creating a reducer action

Let's create an action `handleSelectMail` that pushes a mail into `selectedMails` state.

```ts
import { createSlice } from '@reduxjs/toolkit'

const initialState = {
  selectedMails: []
}

const emailSlice = createSlice({
  name: 'email',
  initialState,
  reducers: {
    handleSelectMail: (state, action) => {
      // You should get mail to select from the action payload. 
      
      const mails = state.selectedMails
      if (!mails.includes(action.payload)) {
        mails.push(action.payload)
      } else {
        mails.splice(mails.indexOf(action.payload), 1)
      }
      state.selectedMails = mails
    }
  }
})

export const { handleSelectMail } = emailSlice.actions

export default appEmailSlice.reducer
```

::: tip Important
The state is a Proxy object, you cannot update it directly, and you have to update its keys instead.

For example: `state = { ...mailData } will break the state, but state.selectedMails = { ...mailData }` works as expected.
:::

## Fetching Data

Use `createAsyncThunk` to fetch data from an api.

```ts
import axios from 'axios'
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit'

const initialState = {
  mails: null
}

// ** Fetch Mails
export const fetchMails = createAsyncThunk('appEmail/fetchMails', async (params) => {
  const response = await axios.get('/apps/email/emails', {
    params
  })

  return { ...response.data, filter: params }
})

const emailSlice = createSlice({
  name: 'email',
  initialState,
  reducers: {},
  extraReducers: builder => {

    // ** update the state.mails when the fetchMails action is fulfilled.
    builder.addCase(fetchMails.fulfilled, (state, action) => {
      state.mails = action.payload.emails
    })      
  }
})

export default appEmailSlice.reducer
```

## Combine the new slice in the root reducer

In the file `src/store/index.ts` use the reducer from your newly created slice.

```ts
import { configureStore } from '@reduxjs/toolkit'

import email from 'src/store/apps/email'

export const store = configureStore({
  reducer: { email },
  middleware: getDefaultMiddleware =>
    getDefaultMiddleware({
      serializableCheck: false
    })    
})
```

## Using the store state

Use `useSelector` hook to access the store state.

```tsx{1,4}
import { useSelector } from 'react-redux'

const Email = () => {
  const store = useSelector(state => state.email)

  return (
    <div>
      {store.mails ? store.mails.map(mail => <div>{mail.id}</div>) : null}
    </div>
  )
}

export default Email
```

## Dispatching an action

Use `useDispatch` hook to dispatch an action.

```tsx{1,5-6,9}
import { useDispatch, useSelector } from 'react-redux'
import { handleSelectMail } from 'src/store/email.ts'

const Email = () => {
  const dispatch = useDispatch()
  const store = useSelector(state => state.email)

  const handleMailClick = mail => {
    dispatch(handleSelectMail(mail))
  }

  return (
    <div>
      {store.mails
        ? store.mails.map(mail => <div onClick={() => handleMailClick(mail)}>{mail.id}</div>)
        : null}
    </div>
  )
}

export default Email
```
