# How to migrate from JWT Auth to NextAuth

::: warning Prerequisite
It is required to have sufficient knowledge of [NextAuth.js](https://next-auth.js.org/) before reading this migration guide
:::

::: tip How to secure API routes?

As the official guide from NextAuth for [securing API routes](https://next-auth.js.org/tutorials/securing-pages-and-api-routes#securing-api-routes) is sufficient, we have not made any separate doc showing the same.

**How to refresh a token?**

If in case you need to implement refresh token functionality in your app, please refer to [this](https://next-auth.js.org/tutorials/refresh-token-rotation) guide from NextAuth.
:::

To remove JWT authentication and implement NextAuth, please follow these steps:

1. Uninstall the `jsonwebtoken` & `@types/jsonwebtoken` packages and install the `next-auth` package using the following command:

   <code-group>
   <code-block title="YARN (Highly Recommended)" active>
   ```bash
   yarn remove jsonwebtoken @types/jsonwebtoken && yarn add next-auth
   ```
   </code-block>

   <code-block title="NPM">
   ```bash
   npm uninstall jsonwebtoken @types/jsonwebtoken && npm install next-auth
   ```
   </code-block>
   </code-group>

2. Delete the `src/@fake-db/auth/jwt.ts`, `src/config/auth.ts`, `src/context/AuthContext.tsx` and `src/hooks/useAuth.tsx` files
3. Remove the `import './auth/jwt'` import statement from the `src/@fake-db/index.ts` file
4. Remove all the types related to the `AuthContext` and user data from the `src/context/types.ts` file. If you have not added any type in this file, you may delete this file
5. If the `src/context` and `src/hooks` folders are empty, delete them
6. Update the Access Control (ACL) guard as the `src/hooks/useAuth.tsx` file has been deleted. It is not recommended to make changes in the `src/@core` folder, so create a new file (say `src/layouts/components/auth/UserAclGuard.tsx`). Copy the code from `src/@core/components/auth/AclGuard.tsx` file, paste it into the new file, and make necessary modifications

   **Change the code from**:

   ```tsx{1,2,5,6}
   import { useAuth } from 'src/hooks/useAuth'
   const auth = useAuth()

   // User is logged in, build ability for the user based on his role
   if (auth.user && auth.user.role && !ability) {
    setAbility(buildAbilityFor(auth.user.role, aclAbilities.subject))
   }
   ```

   **to**:

   ```tsx{1,2,5,6}
   import { useSession } from 'next-auth/react'
   const session = useSession()

   // User is logged in, build ability for the user based on his role
   if (session.data && session.data.user && session.data.user.role && !ability) {
    setAbility(buildAbilityFor(session.data.user.role, aclAbilities.subject))
   }
   ```

7. Update the Authentication guard as the `src/hooks/useAuth.tsx` file has been deleted. It is not recommended to make changes in the `src/@core` folder, so create a new file (say `src/layouts/components/auth/UserAuthGuard.tsx`). Copy the code from `src/@core/components/auth/AuthGuard.tsx` file, paste it into the new file, and make necessary modifications

   **Change the code from**:

   ```tsx{1,2,8,17,20}
   import { useAuth } from 'src/hooks/useAuth'
   const auth = useAuth()

   useEffect(
     () => {
       ...

       if (auth.user === null && !window.localStorage.getItem('userData')) {
         if (router.asPath !== '/') {
           ...
         } else {
           ...
         }
       }
     },
     // eslint-disable-next-line react-hooks/exhaustive-deps
     [router.route]
   )

   if (auth.loading || auth.user === null) {
     return fallback
   }
   ```

   **to**:

   ```tsx{1,2,8,17,20}
   import { useSession } from 'next-auth/react'
   const session = useSession()

   useEffect(
     () => {
       ...

       if (session.status === 'unauthenticated') {
         if (router.asPath !== '/') {
           ...
         } else {
           ...
         }
       }
     },
     // eslint-disable-next-line react-hooks/exhaustive-deps
     [router.route, session.status]
   )

   if (session.status !== 'authenticated') {
     return fallback
   }
   ```

8. Update the Guest guard as the `src/hooks/useAuth.tsx` file has been deleted. It is not recommended to make changes in the `src/@core` folder, so create a new file (say `src/layouts/components/auth/UserGuestGuard.tsx`). Copy the code from `src/@core/components/auth/GuestGuard.tsx` file, paste it into the new file, and make necessary modifications

   **Change the code from**:

   ```tsx{1,2,7,11,13-15,17}
   import { useAuth } from 'src/hooks/useAuth'
   const auth = useAuth()

   useEffect(() => {
     ...

     if (window.localStorage.getItem('userData')) {
       ...
     }
     // eslint-disable-next-line react-hooks/exhaustive-deps
   }, [router.route])

   if (auth.loading || (!auth.loading && auth.user !== null)) {
     return fallback
   }

   return <>{children}</>
   ```

   **to**:

   ```tsx{1,2,7,11,13-17}
   import { useSession } from 'next-auth/react'
   const session = useSession()

   useEffect(() => {
     ...

     if (session.status === 'authenticated' && !router.query.returnUrl) {
       ...
     }
     // eslint-disable-next-line react-hooks/exhaustive-deps
   }, [router.route, session.status])

   if (session.status === 'unauthenticated') {
     return <>{children}</>
   } else {
     return fallback
   }
   ```

9. Update the user dropdown as the `src/hooks/useAuth.tsx` file has been deleted. It is not recommended to make changes in the `src/@core` folder, so create a new file (say `src/layouts/components/UserDropdown.tsx`). Copy the code from `src/@core/layouts/components/shared-components/UserDropdown.tsx` file, paste it into the new file, and make necessary modifications

   **Change the code from**:

   ```tsx{1,2,5}
   import { useAuth } from 'src/hooks/useAuth'
   const { logout } = useAuth()

   const handleLogout = () => {
     logout()
     handleDropdownClose()
   }
   ```

   **to**:

   ```tsx{1,4-6}
   import { signOut } from 'next-auth/react'

   const handleLogout = () => {
     signOut({ callbackUrl: '/', redirect: false }).then(() => {
       router.asPath = '/'
     })
     handleDropdownClose()
   }
   ```

10. Update the import statement in `src/layouts/components/vertical/AppBarContent.{tsx|js}` and/or `src/layouts/components/horizontal/AppBarContent.{tsx|js}` file(s) after creating the new file and making modifications in the previous step

    **from**:

    ```tsx
    import UserDropdown from 'src/@core/layouts/components/shared-components/UserDropdown'
    ```

    **to**:

    ```tsx
    import UserDropdown from 'src/layouts/components/UserDropdown'
    ```

11. As the `src/hooks/useAuth.tsx` file has been deleted, update the code in the `src/pages/login/index.tsx` file according to the NextAuth's provider. We have demonstrated CredentialsProvider and you can find the related code in [this](/articles/nextauth-with-credentials-provider.html#src-pages-login-index-tsx-file) guide

12. Update the `src/pages/_app.tsx` file as the new guards have been created and the `AuthContext` has been removed

    **from**:

    ```tsx{1,2,3,4,6,8}
    import AclGuard from 'src/@core/components/auth/AclGuard'
    import AuthGuard from 'src/@core/components/auth/AuthGuard'
    import GuestGuard from 'src/@core/components/auth/GuestGuard'
    import { AuthProvider } from 'src/context/AuthContext'

    <AuthProvider>
      {...}
    </AuthProvider>
    ```

    **to**:

    ```tsx{1,2,3,4,6,8}
    import AclGuard from 'src/layouts/components/auth/UserAclGuard'
    import AuthGuard from 'src/layouts/components/auth/UserAuthGuard'
    import GuestGuard from 'src/layouts/components/auth/UserGuestGuard'
    import { SessionProvider } from 'next-auth/react'

    <SessionProvider session={pageProps.session}>
      {...}
    </SessionProvider>
    ```

13. Update the `src/pages/index.tsx` file as the `src/hooks/useAuth.tsx` file has been deleted

    **from**:

    ```tsx{1,2,4,5}
    import { useAuth } from 'src/hooks/useAuth'
    const auth = useAuth()

    if (auth.user && auth.user.role) {
      const homeRoute = getHomeRoute(auth.user.role)
      ...
    }
    ```

    **to**:

    ```tsx{1,2,4,5}
    import { useSession } from 'next-auth/react'
    const session = useSession()

    if (session.status === 'authenticated') {
      const homeRoute = getHomeRoute(session.data.user?.role)
      ...
    }
    ```

14. Change the `.env` file

    **from**:

    ```tsx
    NEXT_PUBLIC_JWT_SECRET= YOUR_SECRET_GOES_HERE
    NEXT_PUBLIC_JWT_EXPIRATION= YOUR_EXPIRATION_DURATION_GOES_HERE
    NEXT_PUBLIC_JWT_REFRESH_TOKEN_SECRET= YOUR_REFRESH_TOKEN_SECRET_GOES_HERE
    ```

    **to**:

    ```tsx
    API_URL=http://localhost:3000
    NEXTAUTH_URL=http://localhost:3000
    NEXTAUTH_SECRET= YOUR_SECRET_GOES_HERE
    ```

    You can refer to [this](https://next-auth.js.org/configuration/options#secret) guide for generating your own secret.

15. For `typescript-version` users, add the following in the `tsconfig.json` file:

    ```json{3-5}
    "compilerOptions": {
      "paths": {
        "next-auth": [
          "./node_modules/next-auth"
        ],
        ...
      }
    },
    ```

    You may require the addition of the `next-auth.d.ts` file to your project's root directory to modify certain types specified by NextAuth. A tutorial on how to alter these types is available through the link provided in the next step. If the `next-auth.d.ts` file must be added, the following entry must be included in the `tsconfig.json` file:

    ```json{2}
    "include": [
      "next-auth.d.ts",
      ...
    ],
    ```

16. Create the `src/pages/api/auth/[...nextauth].ts` file. Please refer to [this](/articles/nextauth-with-credentials-provider.html) article on how to implement authentication using [CredentialsProvider](https://next-auth.js.org/providers/credentials). You may customize this file according to your requirements
17. If you get any type errors after doing the above steps, you need to refresh/reopen your editor.

This is it.
