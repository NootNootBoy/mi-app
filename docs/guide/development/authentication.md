# Authentication

::: warning Migrate from JWT auth to NextAuth
Please refer to [this](/articles/how-to-migrate-from-jwt-to-nextauth.html) article if you want to migrate from JWT auth to [NextAuth](https://next-auth.js.org/).
:::

## Overview

We only provide JWT authentication with the template for now. We might integrate other authentication services in future.

## Auth Context

We have created an Authentication context that returns all the necessary functions you might need to authenticate a user like login, logout etc. Please make sure to override context and make necessary changes according to your app requirements. We have created this context for demo purpose only.

## Usage Example

```tsx
import { useAuth } from 'src/hooks/useAuth'

const Component = () => {
  const auth = useAuth()
  const { login, logout } = auth

  const handleErrCallback = err => {
    console.log(err)
  }

  const handleLogin = () => {
    login({ email, password, rememberMe }, err => handleErrCallback(err))
  }

  return (
    <Form>
      ...
      <Button onClick={handleLogin}>Login</Button>
      <Button onClick={logout}>logout</Button>
    </Form>
  )
}

export default Component
```

## Overriding Auth

We are using `localStorage` & `fake-db` to store tokens and authenticate the user.
In a real application, you might store the token & user data in a `session` or `cookies`.

Follow these steps to override the auth context:

1. Open `src/context/AuthContext.tsx` file
2. Now update the authentication code according to your authentication logic
3. That's it now you can use your modified context.

## Auth Context Values

| Property         | Type     | Description                                     |
| ---------------- | :------- | ----------------------------------------------- |
| user             | Object   | LoggedIn User Object                            |
| setUser          | Function | Function to update LoggedIn User                |
| isInitialized    | Boolean  | Returns if authentication is initialized or not |
| setIsInitialized | Function | Function to update isInitialized state          |
| loading          | Boolean  | Returns if app is loading                       |
| setLoading       | Function | Function to update loading state                |
| login            | Function | Function to login user.                         |
| logout           | Function | Function to logout user.                        |

## Securing Pages

We have created a wrapper that checks for the authentication status and redirects user if not logged in.

There are two types of guards:

- **AuthGuard**
- **GuestGuard**

Default value for both guards are as follows:

- **authGuard: true**
- **guestGuard: false**

User don't have to define `AuthGuard` or `GuestGuard` on all the pages as we have already defined default values as above.

Now let's consider scenarios where we need to override `AuthGuard` & `GuestGuard`.

### Guest Guard

For public pages like Login, Registration, Forgot Password, etc., we need to set GuestGuard value to true, as we don't want already logged in user to visit those pages and only guest should be able to visit those pages.

Setting GuestGuard to true in LoginPage component. Visit `src/pages/login/index.tsx` to see it in the action and find out where and how to configure / override `guestGuard`.

```tsx
LoginPage.guestGuard = true
```

Setting GuestGuard to true will redirect already logged in user to home page whenever they try to visit the public pages like Login. So make sure to only change / override guestGuard when you do not want logged in users to visit that page.

### Auth Guard

Now, let's consider error pages, coming soon, under maintenance or common pages which is accessible by both guest and logged in users. User just need to set authGuard to false to do the same.

Setting authGuard to false in ComingSoon page component:

```tsx
ComingSoon.authGuard = false
```

Setting authGuard to false will allow all the users to visit that page whether logged in or not.

If you want to show menu items in the navigation menu for the logged out user as well, it is necessary to add the `auth: false` parameter in `@src/navigation/vertical/index.tsx` and/or `@src/navigation/horizontal/index.tsx` file(s).

If a single link is to be displayed, `auth` property should be added solely to the corresponding menu link. If a link is to be displayed which is in a sub-menu, then the `auth` property must be added to both the link and the submenu. Additionally, if a section title is to be displayed for number of links and/or groups, then `auth` property must be added to the section title as well.

Refer to the example below:

```tsx{7,16,21,25}
[
  {
    title: 'Dashboards',
    icon: 'mdi:home-outline',
    badgeContent: 'new',
    badgeColor: 'error',
    auth: false,
    children: [
      {
        title: 'Analytics',
        path: '/dashboards/analytics'
      },
      {
        title: 'eCommerce',
        path: '/dashboards/ecommerce',
        auth: false
      }
    ]
  },
  {
    auth: false,
    sectionTitle: 'Apps & Pages'
  },
  {
    auth: false,
    title: 'Email',
    icon: 'mdi:email-outline',
    path: '/apps/email'
  },
]
```

## onTokenExpiration

We provide `onTokenExpiration` property in `src/configs/auth`. It decides what action should take place when issued token is expired.

| Value             |Description                                          |
| ----------------  | -----------------------------------------------     |
| logout            | will logout and redirect the user to `/login` page. |
| refreshToken      | will generate new token for the current user.       |

::: warning Note
Because we're storing data in localStorage when you change the `onTokenExpiration` you'll have to clear the localStorage and login again.
:::

## JWT Token

We sign the user token in `src/@fake-db/auth/jwt.js` file.

The `jwtConfig` object contains three things `expirationTime`, `secret` `refreshTokenSecret`.

| Value               |Description                                     |
| ----------------    | -----------------------------------------------|
| expirationTime      | User token expiration time                     |
| secret              | JWT secret to sign accessToken                 |
| refreshTokenSecret  | JWT secret to sign refreshToken                |

As shown in the above section you can either `logout` the user or `referToken` on token expiration.
You can find the logic for that `'/auth/me'` onGet request in the same file.

You can use `jwt.verify` function to check for token validity and create a function according to your needs.

Here's how we have used `jwt.verify`: 

```js
mock.onGet('/auth/me').reply(config => { 
  // Get token from header
  const token = config.headers.Authorization

  // Default response
  let response: ResponseType = [200, {}]

  // Checks if the token is valid or expired
  jwt.verify(token, jwtConfig.secret, (err, decoded) => {
    // If token is expired
    if (err) {
      // If onTokenExpiration === 'logout' then send 401 error
      if (defaultAuthConfig.onTokenExpiration === 'logout') {
        response = [401, { error: { error: 'Invalid User' } }]
      } else {
        // If onTokenExpiration === 'refreshToken' then generate the new token
        const oldTokenDecoded = jwt.decode(token, { complete: true })
        
        // Get user id from old token
        const { id: userId } = oldTokenDecoded.payload

        // Get user that matches id in token
        const user = users.find(u => u.id === userId)
        
        // Sign a new token
        const accessToken = jwt.sign({ id: userId }, jwtConfig.secret, { expiresIn: jwtConfig.expirationTime })

        // Set new token in localStorage
        window.localStorage.setItem(defaultAuthConfig.storageTokenKeyName, accessToken)

        const obj = { userData: { ...user, password: undefined } }

        // return 200 with user data
        response = [200, obj]
      }
    } else {
      // If token is valid do nothing      
      const userId = decoded.id

      // Get user that matches id in token
      const userData = JSON.parse(JSON.stringify(users.find((u: UserDataType) => u.id === userId)))

      delete userData.password

      // return 200 with user data
      response = [200, { userData }]
    }
  })

  // Send Response 
  return response
})

```

## How to remove Authentication

Removing the authentication from the app is simple.

If you want to remove authentication from your project, there will be no point of giving access to users according to their role. Thus, you need to remove Access Control (ACL) from the project. Please refer to [this](/guide/development/access-control.html#how-to-remove-acl) doc to remove ACL.

Now, follow the steps given below to remove authentication from your project.

**Changes in `scr/pages/_app.tsx` file**

1. Remove all Auth related import statements

    ```tsx
    import { ReactNode } from 'react'
    import AuthGuard from 'src/@core/components/auth/AuthGuard'
    import GuestGuard from 'src/@core/components/auth/GuestGuard'
    import Spinner from 'src/@core/components/spinner'
    import { AuthProvider } from 'src/context/AuthContext'
    ```

2. Remove the `Guard` Component and its wrapper
3. Remove the wrapper of the `AuthProvider` component
4. Remove the `authGuard` & `guestGuard` variables
5. Remove the `GuardProps` type

---

**Changes in other files**

1. Remove `src/@core/components/auth` folder
2. Search and remove `Component.guestGuard` & `Component.authGuard` methods from all the files (where Component is the name of the component)
3. Remove `authGuard?: boolean` and `guestGuard?: boolean` from the `next.d.ts` file
4. Remove the `src/@fake-db/auth` folder and the `import './auth/jwt'` import statement from the file `src/@fake-db/index.ts`
5. Remove `src/context/AuthContext.tsx` & all types related to the Auth from the `src/context/types.ts` file and their import statements & their usage inside `src` folder
6. Remove `src/hooks/useAuth.tsx` file and its import statements & their usage inside `src` folder
7. If you want the user dropdown in the appBar, you need to override that component in `src/@core/layouts/components/shared-components/UserDropdown.tsx` file. If you do not require the user dropdown, then remove `src/@core/layouts/components/shared-components/UserDropdown.tsx` file, its import statements and its usage in `src/layouts/components/vertical/AppBarContent.tsx`  and `src/layouts/components/horizontal/AppBarContent.tsx` files

**That's it. Now your app is auth free.**
