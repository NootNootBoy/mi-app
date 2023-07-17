# How to replace API endpoints

In your app, you would want to use the real APIs instead of one created with the FakeDB.

To replace the APIs with the real ones, make sure you have created the APIs in your backend & connected the APIs with your database.

::: warning NOTE
If the structure of the data you receive from the API is different than ours, then you'll have to update the app structure too.

You can refer to the data structure in the `src/fake-db/` folder.
:::

## Apps/Pages

You can find the API usage for all the apps in the `src/store/apps` folder & API usage for pages in their respective page folders

Let's take the Invoice App as an example to replace the API.

Follow these steps to replace the API for the invoice app:

1. Open `src/store/apps/invoice/index.{ts|js}` and replace the API in the `createAsyncThunk` function
2. You can also use your editor to find the APIs in the whole template & replace them accordingly

## Authentication

For Authentication, all the necessary APIs can be found in the `src/configs/auth.ts` file. Instead of searching and replacing individual Authentication APIs, simply update the exported object to update all the relevant APIs.
