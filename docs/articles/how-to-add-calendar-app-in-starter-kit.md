# How to add Calendar App in starter-kit

Sneat uses [fullcalendar](https://fullcalendar.io/docs#toc) for Calendar App. Follow these steps to integrate Calendar in starter-kit:

1. Create a `store/apps` folder in `src/`
2. Copy Calendar folder from `full-version/src/store/apps/` to `starter-kit/src/store/apps/`
3. Create `index.ts` file in `store` folder and add the following code:

```jsx
// ** Toolkit imports
import { configureStore } from '@reduxjs/toolkit'

import calendar from 'src/store/apps/calendar'

export const store = configureStore({
  reducer: { calendar },
  middleware: getDefaultMiddleware =>
    getDefaultMiddleware({
      serializableCheck: false
    })
})

export type RootState = ReturnType<typeof store.getState>
```

4. Navigate to `src/pages/_app.tsx` & add the following imports

```jsx
// ** Store Imports
import { store } from 'src/store'
import { Provider } from 'react-redux'
```

5. Wrap your app with `<Provider store={store}>` to get access to the redux store.
6. Create a `@fake-db` folder.
7. Create `mock.ts` file in the newly created `@fake-db` folder and add the following code:

```jsx
import axios from 'axios'
import MockAdapter from 'axios-mock-adapter'

const mock = new MockAdapter(axios)

export default mock
```

8. Create a `apps` folder in the `@fake-db` and copy `full-version/src/@fake-db/apps/calendar.ts` file to the `@fake-db/apps` folder.
9. Create `index.ts` file in the `@fake-db` folder and add the following code:

```jsx
import mock from './mock'

import './apps/calendar'

mock.onAny().passThrough()
```

10. Add the following import in `src/pages/_app.tsx`:

```jsx
// ** Fake-DB Import
import 'src/@fake-db'
```

11. Copy `full-version/src/views/apps/calendar` folder to `starter-kit/src/views/apps/calendar`
12. Copy `full-version/src/pages/apps/calendar` folder to `starter-kit/src/pages/apps/calendar`
13. Finally add the calendar in `src/navigation/vertical/index.ts` and `src/navigation/horizontal/index.ts`:

```jsx
const navigation = () => {
  return [
    ...
    {
      title: 'Calendar',
      path: '/apps/calendar',
      icon: 'mdi:calendar-blank-outline'
    },
    ...
  ]
}
```
