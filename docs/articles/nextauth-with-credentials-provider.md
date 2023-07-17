# NextAuth with CredentialsProvider

Please find below a guide for authentication with NextAuth using only the [CredentialsProvider](https://next-auth.js.org/providers/credentials). Additional providers may be added or removed as per your specific requirements.

For your convenience, each functional aspect has been thoroughly commented and accompanied by valuable insights and relevant links that will assist you in customizing your authentication process to align with your specific needs.

Please note that customization of NextAuth to meet specific requirements, such as modifying the session strategy, adjusting session expiration times, designating authentication pages, and customizing callback functions, are not considered part of the support. These elements will vary based on the specific implementation.

## `[...nextauth].ts` file

The implementation of the authentication logic should be performed within the `src/pages/api/auth/[...nextauth].ts` file. It is advisable to tailor this file to suit the specific requirements of your project. The necessary configurations and instructions for customizing can be located in the [NextAuth official documentation](https://next-auth.js.org/configuration/initialization).

<code-group>
<code-block title="TS" active>
```ts
// ** Third Party Imports
import NextAuth, { NextAuthOptions } from 'next-auth'
import CredentialsProvider from 'next-auth/providers/credentials'

/*
 * As we do not have backend server, the refresh token feature has not been incorporated into the template.
 * Please refer https://next-auth.js.org/tutorials/refresh-token-rotation link for a reference.
 */

export const authOptions: NextAuthOptions = {
  // ** Configure one or more authentication providers
  // ** Please refer to https://next-auth.js.org/configuration/options#providers for more `providers` options
  providers: [
    CredentialsProvider({
      // ** The name to display on the sign in form (e.g. 'Sign in with...')
      name: 'Credentials',
      type: 'credentials',

      /*
       * As we are using our own Sign-in page, we do not need to change
       * username or password attributes manually in following credentials object.
       */
      credentials: {},
      async authorize(credentials) {
        /*
         * You need to provide your own logic here that takes the credentials submitted and returns either
         * an object representing a user or value that is false/null if the credentials are invalid.
         * For e.g. return { id: 1, name: 'J Smith', email: 'jsmith@example.com' }
         * You can also use the `req` object to obtain additional parameters (i.e., the request IP address)
         */
        const { email, password } = credentials as { email: string; password: string }

        try {
          // ** Login API Call to match the user credentials and receive user data in response along with his role
          const res = await fetch(`${process.env.API_URL}/api/login`, {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify({ email, password })
          })
          const user = await res.json()

          if (res.status === 200 && user) {
            /*
             * Please unset all the sensitive information of the user either from API response or before returning
             * user data below. Below return statement will set the user object in the token and the same is set in
             * the session which will be accessible all over the app.
             */
            return user
          }

          return null
        } catch {
          throw new Error('Email or Password is invalid')
        }
      }
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
import CredentialsProvider from 'next-auth/providers/credentials'

/*
 * As we do not have backend server, the refresh token feature has not been incorporated into the template.
 * Please refer https://next-auth.js.org/tutorials/refresh-token-rotation link for a reference.
 */

export const authOptions = {
  // ** Configure one or more authentication providers
  // ** Please refer to https://next-auth.js.org/configuration/options#providers for more `providers` options
  providers: [
    CredentialsProvider({
      // ** The name to display on the sign in form (e.g. 'Sign in with...')
      name: 'Credentials',
      type: 'credentials',

      /*
       * As we are using our own Sign-in page, we do not need to change
       * username or password attributes manually in following credentials object.
       */
      credentials: {},
      async authorize(credentials) {
        /*
         * You need to provide your own logic here that takes the credentials submitted and returns either
         * an object representing a user or value that is false/null if the credentials are invalid.
         * For e.g. return { id: 1, name: 'J Smith', email: 'jsmith@example.com' }
         * You can also use the `req` object to obtain additional parameters (i.e., the request IP address)
         */
        const { email, password } = credentials

        try {
          // ** Login API Call to match the user credentials and receive user data in response along with his role
          const res = await fetch(`${process.env.API_URL}/api/login`, {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify({ email, password })
          })
          const user = await res.json()

          if (res.status === 200 && user) {
            /*
             * Please unset all the sensitive information of the user either from API response or before returning
             * user data below. Below return statement will set the user object in the token and the same is set in
             * the session which will be accessible all over the app.
             */
            return user
          }

          return null
        } catch {
          throw new Error('Email or Password is invalid')
        }
      }
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

We utilize the [CredentialsProvider](https://next-auth.js.org/providers/credentials) which enables the handling of sign-in through diverse credentials, such as a username and password. Multiple authentication providers can be configured simultaneously.

Please refer to [this](https://cloudcoders.xyz/blog/nextauth-credentials-provider-with-external-api-and-login-page) example for the comprehension of implementing NextAuth with actual APIs via CredentialsProvider.

The following options are available within CredentialsProvider:

#### *name*

The name to display on the sign in form (e.g. 'Sign in with...')

#### *type*

Type of provider, in this case credentials

#### *credentials*

The credentials to sign-in with. As we are employing our own Sign-in page, we do not need to change username or password attributes manually in the credentials.

#### *authorize*

Callback to execute once user is to be authorized.

You need to provide your own logic here that takes the credentials submitted and returns either an object representing a user or value that is false/null if the credentials are invalid. For e.g. return `{ id: 1, name: 'J Smith', email: 'jsmith@example.com' }`. You can also use the `req` object to obtain additional parameters (i.e., the request IP address).

::: warning
To match the user credentials, you must make a call to the login API to receive the user data in response. It is imperative to securely remove all sensitive information from the user data, either from the API response or before returning the user data to ensure confidentiality.
:::

Kindly consult the official [NextAuth documentation](https://next-auth.js.org/configuration/options#providers) for more `providers` options.

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

## Login API

Please create your login API, where the authentication of the user's credentials will take place.

Here is the example code of it for the `src/pages/api/login/index.ts` file:

<code-group>
<code-block title="TS" active>
```ts
// ** Next Imports
import { NextApiResponse, NextApiRequest } from 'next/types'

// ** Fake user data and data type
// ** Please remove below user data and data type in production and verify user with Real Database
export type UserDataType = {
  id: number
  role: string
  email: string
  fullName: string
  username: string
  password: string
}
const users: UserDataType[] = [
  {
    id: 1,
    role: 'admin',
    password: 'admin',
    username: 'johndoe',
    fullName: 'John Doe',
    email: 'admin@sneat.com'
  },
  {
    id: 2,
    role: 'client',
    password: 'client',
    username: 'nathandoe',
    fullName: 'Nathan Doe',
    email: 'client@sneat.com'
  }
]

const handler = (req: NextApiRequest, res: NextApiResponse) => {
  const { email, password } = req.body

  const user = users.find(u => u.email === email && u.password === password)

  if (user) {
    return res.status(200).json(user)
  } else {
    return res.status(404).json({ message: 'Email or Password is invalid' })
  }
}

export default handler
```
</code-block>

<code-block title="JS">
```js
// ** Fake user data
// ** Please remove below user data in production and verify user with Real Database
const users = [
  {
    id: 1,
    role: 'admin',
    password: 'admin',
    username: 'johndoe',
    fullName: 'John Doe',
    email: 'admin@sneat.com'
  },
  {
    id: 2,
    role: 'client',
    password: 'client',
    username: 'nathandoe',
    fullName: 'Nathan Doe',
    email: 'client@sneat.com'
  }
]

const handler = (req, res) => {
  const { email, password } = req.body

  const user = users.find(u => u.email === email && u.password === password)

  if (user) {
    return res.status(200).json(user)
  } else {
    return res.status(404).json({ message: 'Email or Password is invalid' })
  }
}

export default handler
```
</code-block>
</code-group>

## `next-auth.d.ts` file

It may be necessary to include the `next-auth.d.ts` file in the root directory of your project to modify certain types specified by NextAuth.

In this example, the `role` and `fullName` options have been added to the user's object. The following type declaration can be added to extend NextAuth's types:

```ts
import 'next-auth/jwt'
import { DefaultSession } from 'next-auth'

declare module 'next-auth/jwt' {
  interface JWT {
    role: string
    fullName: string
  }
}

declare module 'next-auth' {
  interface Session {
    user: {
      role: string
      fullName: string
    } & DefaultSession['user']
  }

  interface User {
    role: string
    fullName: string
  }
}
```

You may customize this file to meet your specific requirements.

## `src/pages/login/index.tsx` file

During the migration process from JWT auth to NextAuth, the `src/hooks/useAuth.tsx` file has been removed, causing an error in the `src/pages/login/index.tsx` file. To rectify the issue, kindly update this file

**from**:

```tsx{1,3,7-12}
import { useAuth } from 'src/hooks/useAuth'

const auth = useAuth()

const onSubmit = (data: FormData) => {
 const { email, password } = data
 auth.login({ email, password }, () => {
   setError('email', {
     type: 'manual',
     message: 'Email or Password is invalid'
   })
 })
}
```

**to**:

```tsx{1,2,4,8-20}
import { useRouter } from 'next/router'
import { signIn } from 'next-auth/react'

const router = useRouter()

const onSubmit = (data: FormData) => {
const { email, password } = data
 signIn('credentials', { email, password, redirect: false }).then(res => {
   if (res && res.ok) {
     const returnUrl = router.query.returnUrl
     const redirectURL = returnUrl && returnUrl !== '/' ? returnUrl : '/'

     router.replace(redirectURL as string)
   } else {
     setError('email', {
       type: 'manual',
       message: 'Email or Password is invalid'
     })
   }
 })
}
```

You may customize this file to meet your specific requirements.
