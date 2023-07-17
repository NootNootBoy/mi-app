# FakeDB

Sneat is built using FakeDB to mock the real life application functionalities.

## Overview

Sneat uses [axios-mock-adapter](https://github.com/ctimmerm/axios-mock-adapter) to simulate the server calls.

All of the server calls are located in `src/@fake-db`.

## Setup

If you're using the starter-kit you'll have to manually setup the fake-db.

1. First create a folder with name `fake-db` and create a `mock.ts` file inside it.
2. Initialize the axios-mock-adapter in `mock.ts` file.

   ```ts
   import axios from 'axios'
   import MockAdapter from 'axios-mock-adapter'

   const mock = new MockAdapter(axios)

   export default mock
   ```

3. Create a `index.ts` file in `fake-db` folder & add the following:

   ```ts
   import mock from './mock'

   mock.onAny().passThrough()
   ```

4. To initialize your fake data create a ts file in `fake-db` folder. Import `mock` and use it like following:

   ```ts
   import mock from '../mock'

   const data = [{...}]

   mock.onGet('/url/get-data').reply(config => {
     return [200, data]
   })
   ```

5. Import the above created file in `fake-db/index.ts`:

   ```ts
   import mock from './mock'

   import './FILE_WITH_DATA'

   mock.onAny().passThrough()
   ```

6. Import your `fake-db/index.ts` in `src/pages/_app_.ts` to be able to get your data in your app.

7. Finally, use axios to fetch your data from fake-db

```ts
import { useState, useEffect } from 'react'

import axios from 'axios'

const Component = () => {
  const [data, setData] = useState([])

  useEffect(() => {
    axios.get('/url/get-data').then(response => setData(response.data))
  }, [])

  return <h1>Component</h1>
}
```

::: warning
We have used the fake-db for demo purposes only. fake-db will not work for the real life applications.
:::
