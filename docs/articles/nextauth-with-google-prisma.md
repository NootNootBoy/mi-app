# NextAuth with Google Provider and Prisma Adapter

Please find below a guide for authentication with NextAuth using only the [GoogleProvider](https://next-auth.js.org/providers/google) and [PrismaAdapter](https://next-auth.js.org/adapters/prisma). Additional providers may be added or removed as per your specific requirements.

For your convenience, each functional aspect has been thoroughly commented and accompanied by valuable insights and relevant links that will assist you in customizing your authentication process to align with your specific needs.

Please note that customization of NextAuth to meet specific requirements, such as modifying the session strategy, adjusting session expiration times, designating authentication pages, and customizing callback functions, are not considered part of the support. These elements will vary based on the specific implementation.

## Connect your project with Google Cloud

Please follow the instructions below to set up your Google Cloud account:

Open the Google Cloud Console using [this](https://console.developers.google.com/apis/credentials) link.

If you have multiple projects on Google Cloud, select any one to connect with your project, or create a new one.

Follow the complete setup guide for Google Cloud by referring to [this](https://youtu.be/A5ZN--P9vXM) video link.

When creating your credentials, ensure that the "Authorized redirect URIs" include your full domain and end in the callback path. For example:

- For production: `https://{YOUR_DOMAIN}/api/auth/callback/google`
- For development: `http://localhost:3000/api/auth/callback/google`

After creating the OAuth client, you will be provided with a `CLIENT_ID` and `CLIENT_SECRET` by Google Cloud Console. Store these in your `.env` file or as per your requirement as shown below:

```tsx
GOOGLE_CLIENT_ID= YOUR_CLIENT_ID_GOES_HERE // your CLIENT_ID provided by Google Cloud Console
GOOGLE_CLIENT_SECRET= YOUR_CLIENT_SECRET_GOES_HERE // your CLIENT_SECRET provided by Google Cloud Console
```

## Prisma Adapter Setup

::: warning
If you are using SQLite database with Prisma, then you need to remove `@db.Text` text from the `prisma/schema.prisma` file.
:::

Please follow all the steps provided in the official NextAuth's [PrismaAdapter](https://next-auth.js.org/adapters/prisma).

The necessary files, `lib/prismadb.ts` and `prisma/schema.prisma`, can be found in above link. You may move these files as per your requirements. In this example, we kept these files in the `src` folder.

::: tip Note!
Please note that you must change the import path of `lib/prismadb.ts` in the `pages/api/auth/[...nextauth].js` file to match its new location.
:::

In the `schema.prisma` file, we used `SQLite` database as the provider, with `file:./dev.db` specified as the URL in the `datasource db`. Here is the example code:

```tsx
datasource db {
  provider = "sqlite"
  url      = "file:./dev.db"
}
```

However, you may alter the above settings to as per your database.

You are free to add or remove tables and columns as per your requirements. In this example, a `role` column has been added to the `User` table to define the role of a user. Please refer to the following code to add the same:

```tsx
model User {
  id            String    @id @default(cuid())
  name          String?
  email         String?   @unique
  emailVerified DateTime?
  image         String?
  accounts      Account[]
  sessions      Session[]
  role          String?  @default("admin")
}
```

After saving your schema, use the Prisma CLI to generate the Prisma Client by running the following command in the `src` folder for this example:

```bash
npx prisma generate
```

To configure your database to use the new schema (e.g. creating tables and columns), run the following command using the Prisma CLI in the `src` folder for this example:

```bash
npx prisma migrate dev
```

If you want to watch the preview of the Prisma database, you may run the following command:

```bash
npx prisma studio
```

## `[...nextauth].ts` file

The implementation of the authentication logic should be performed within the `src/pages/api/auth/[...nextauth].ts` file. It is advisable to tailor this file to suit the specific requirements of your project. The necessary configurations and instructions for customizing can be located in the [NextAuth official documentation](https://next-auth.js.org/configuration/initialization).

<code-group>
<code-block title="TS" active>
```ts
// ** Third Party Imports
import NextAuth, { NextAuthOptions } from 'next-auth'
import GoogleProvider from 'next-auth/providers/google'
import { PrismaAdapter } from '@next-auth/prisma-adapter'
import prisma from '../../../lib/prismadb'

/*
* As we do not have backend server, the refresh token feature has not been incorporated into the template.
* Please refer https://next-auth.js.org/tutorials/refresh-token-rotation link for a reference.
 */

export const authOptions: NextAuthOptions = {
  adapter: PrismaAdapter(prisma),

  // ** Configure one or more authentication providers
  // ** Please refer to https://next-auth.js.org/configuration/options#providers for more `providers` options
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID as string,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET as string
    })

    // ** ...add more providers here
  ],

  // ** Please refer to https://next-auth.js.org/configuration/options#session for more `session` options
  session: {
    /*
     * Choose how you want to save the user session.
     * The default is `jwt`, an encrypted JWT (JWE) stored in the session cookie.
     * If you use an `adapter` however, NextAuth default it to `database` instead.
     * You can still force a JWT session by explicitly defining `jwt`.
     * When using `database`, the session cookie will only contain a `sessionToken` value,
     * which is used to look up the session in the database.
     */
    strategy: 'jwt',

    // ** Seconds - How long until an idle session expires and is no longer valid
    maxAge: 30 * 24 * 60 * 60 // ** 30 days
  },

  // ** Please refer to https://next-auth.js.org/configuration/options#pages for more `pages` options
  pages: {
    signIn: '/login',
    signOut: '/login',
    error: '/404'
  },

  // ** Please refer to https://next-auth.js.org/configuration/options#callbacks for more `callbacks` options
  callbacks: {
    /*
     * While using `jwt` as a strategy, `jwt()` callback will be called before
     * the `session()` callback. So we have to add custom parameters in `token`
     * via `jwt()` callback to make them accessible in the `session()` callback
     */
    async jwt({ token, user }) {
      if (user) {
        /*
         * For adding custom parameters to user in session, we first need to add those parameters
         * in token which then will be available in the `session()` callback
         */
        token.role = user.role
        token.fullName = user.fullName
      }

      return token
    },
    async session({ session, token }) {
      if (session.user) {
        // ** Add custom params to user in session which are added in `jwt()` callback via `token` parameter
        session.user.role = token.role
        session.user.fullName = token.fullName
      }

      return session
    }
  }
}

export default NextAuth(authOptions)
```
</code-block>

<code-block title="JS">
```js
// ** Third Party Imports
import NextAuth from 'next-auth'
import GoogleProvider from 'next-auth/providers/google'
import { PrismaAdapter } from '@next-auth/prisma-adapter'
import prisma from '../../../lib/prismadb'

/*
 * As we do not have backend server, the refresh token feature has not been incorporated into the template.
 * Please refer https://next-auth.js.org/tutorials/refresh-token-rotation link for a reference.
 */

export const authOptions = {
  adapter: PrismaAdapter(prisma),

  // ** Configure one or more authentication providers
  // ** Please refer to https://next-auth.js.org/configuration/options#providers for more `providers` options
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET
    })
    // ** ...add more providers here
  ],

  // ** Please refer to https://next-auth.js.org/configuration/options#session for more `session` options
  session: {
    /*
     * Choose how you want to save the user session.
     * The default is `jwt`, an encrypted JWT (JWE) stored in the session cookie.
     * If you use an `adapter` however, NextAuth default it to `database` instead.
     * You can still force a JWT session by explicitly defining `jwt`.
     * When using `database`, the session cookie will only contain a `sessionToken` value,
     * which is used to look up the session in the database.
     */
    strategy: 'jwt',

    // ** Seconds - How long until an idle session expires and is no longer valid
    maxAge: 30 * 24 * 60 * 60 // ** 30 days
  },

  // ** Please refer to https://next-auth.js.org/configuration/options#pages for more `pages` options
  pages: {
    signIn: '/login',
    signOut: '/login',
    error: '/404'
  },

  // ** Please refer to https://next-auth.js.org/configuration/options#callbacks for more `callbacks` options
  callbacks: {
    /*
     * While using `jwt` as a strategy, `jwt()` callback will be called before
     * the `session()` callback. So we have to add custom parameters in `token`
     * via `jwt()` callback to make them accessible in the `session()` callback
     */
    async jwt({ token, user }) {
      if (user) {
        /*
         * For adding custom parameters to user in session, we first need to add those parameters
         * in token which then will be available in the `session()` callback
         */
        token.role = user.role
        token.fullName = user.fullName
      }

      return token
    },
    async session({ session, token }) {
      if (session.user) {
        // ** Add custom params to user in session which are added in `jwt()` callback via `token` parameter
        session.user.role = token.role
        session.user.fullName = token.fullName
      }

      return session
    }
  }
}

export default NextAuth(authOptions)
```
</code-block>
</code-group>
In order to successfully customize the file, it is recommended to understand its contents and how it functions. Allow us to commence.

::: tip Note
All the options used in the above `[...nextauth].ts` file are outlined and explained below. Please refer to the official [NextAuth documentation](https://next-auth.js.org/configuration/options) for a comprehensive list of available options.
:::

### providers

---

We utilize the [GoogleProvider](https://next-auth.js.org/providers/google) which enables the handling of sign-in through google. Multiple authentication providers can be configured simultaneously.

The following options are available within GoogleProvider:

#### *clientId*

The `client ID` provided by Google Cloud Console

#### *clientSecret*

The `client secret` provided by Google Cloud Console

Kindly consult the official [NextAuth documentation](https://next-auth.js.org/configuration/options#providers) for more providers options.

### secret

---

It is a random string used to hash tokens, sign/encrypt cookies and generate cryptographic keys.

If the `NEXTAUTH_SECRET` is set as an environment variable, it is not necessary to define this option. A secret can be generated by visiting the documentation link provided below.

Kindly consult the official [NextAuth documentation](https://next-auth.js.org/configuration/options#secret) for more details on `secret`.

### session

---

#### *strategy*

You are required to make a choice on how you wish to preserve the user session. The default option is `jwt`, which involves the storage of an encrypted JWT (JWE) within a session cookie. If you elect to use an `adapter`, the default setting will be changed to `database` instead. It is still possible to explicitly specify `jwt` and retain a JWT session. If the option `database` is chosen, the session cookie will only hold a `sessionToken` value, which will then be used to retrieve the session information from the database.

#### *maxAge*

The duration of an idle session until it expires and becomes invalid. It accepts a number in seconds.

Kindly consult the official [NextAuth documentation](https://next-auth.js.org/configuration/options#session) for more `session` options.

### pages

---

Specify URLs to be used if you want to create custom sign in, sign out and error pages. Pages specified will override the corresponding built-in page.

Kindly consult the official [NextAuth documentation](https://next-auth.js.org/configuration/options#pages) for more `pages` options.

### callbacks

---

Callbacks are asynchronous functions you can use to control what happens when an action is performed. Callbacks are extremely powerful, especially in scenarios involving JSON Web Tokens as they allow you to implement access controls without a database and to integrate with external databases or APIs.

#### *jwt*

This callback is called whenever a JSON Web Token is created (i.e. at sign in) or updated (i.e whenever a session is accessed in the client). The returned value will be encrypted, and it is stored in a cookie.

When utilizing the `jwt` strategy within the `session` option, the `jwt()` callback will be executed prior to the `session()` callback. The data returned by the `authorize` function in the `providers` option will be passed to the `jwt()` callback in the form of the `token`.

To include custom parameters in the `session()` callback, they must be added to the `token` in the `jwt()` callback, which will then be transferred to the `session()` callback for further processing.

Kindly consult the official [NextAuth documentation](https://next-auth.js.org/configuration/callbacks#jwt-callback) for more details on `jwt()` callback.

#### *session*

The session callback is called whenever a session is checked. By default, **only a subset of the token is returned for increased security**. If you want to make something available you added to the token (like `access_token` and `user.id` from above) via the `jwt()` callback, you have to explicitly forward it here to make it available to the client.

Kindly consult the official [NextAuth documentation](https://next-auth.js.org/configuration/callbacks#session-callback) for more details on `session()` callback.

Kindly consult the official [NextAuth documentation](https://next-auth.js.org/configuration/options#callbacks) for more `callbacks` options.

<br />

We hope that with the information provided, you have now acquired a comprehensive understanding of all the options available within the `[...nextauth].ts` or `[...nextauth].js` file.

## `next-auth.d.ts` file

It may be necessary to include the `next-auth.d.ts` file in the root directory of your project to modify certain types specified by NextAuth.

In this example, the `role` option have been added to the user's object. The following type declaration can be added to extend NextAuth's types:

```ts
import 'next-auth/jwt'
import { DefaultSession } from 'next-auth'

declare module 'next-auth/jwt' {
  interface JWT {
    role: string
  }
}

declare module 'next-auth' {
  interface Session {
    user: {
      role: string
    } & DefaultSession['user']
  }

  interface User {
    role: string
  }
}
```

You may customize this file to meet your specific requirements.

### Login Page

To login with Google, add a button like bellow:

```tsx
import { signIn } from 'next-auth/react'

<Button fullWidth size='large' sx={{ mb: 7 }} variant='contained' onClick={() => signIn('google')}>
  Login with google
</Button>
```

### Useful Links

To implement Prisma (SQLite) with Next.js, check out [this](https://youtu.be/FMnlyi60avU) video.

To implement NextAuth with PrismaAdapter (Planetscale), check out [this](https://youtu.be/zB7u1r0tc6o) video.

To implement NextAuth with [CredentialProvider](https://next-auth.js.org/configuration/providers/credentials), refer to [this](/articles/nextauth-with-credentials-provider.html) article.
