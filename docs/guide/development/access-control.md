# Access Control (ACL)

## Overview

Sneat uses the [CASL](https://casl.js.org/v5/en/) package to provide access control. CASL is future-oriented and is more detailed on Access Control.

We suggest you read the [CASL](https://casl.js.org/v5/en/) documentation to learn how it works.

CASL may look complex at first so please make sure you first read their docs carefully and understand the base logic of Access Control to proceed further.

## Config

You can find CASL configuration in `src/configs/acl.ts`.

We have defined two roles `admin` & `client` and their actions in the configuration file.

You'll have to update these roles & actions according to your application requirement.

```ts
const defineRulesFor = (role, subject) => {
  const { can, rules } = new AbilityBuilder(AppAbility)

  if (role === 'admin') {
    can('manage', 'all')
  } else if (role === 'client') {
    can(['read'], 'acl-page')
  } else {
    can(['read', 'create', 'update', 'delete'], subject)
  }

  return rules
}
```

## Component

To define an accessible component use `acl` method with `action` & `subject` properties like shown below.

You can also refer `full-version/src/pages/acl/index.tsx` file for implementation.

```tsx{3-6}
const Component = () => <h1>Component</h1>

Component.acl = {
  action: 'read',
  subject: 'component'
}

export default Component
```

## Navigation

Define the `action` & `subject` properties in navigation file to show/hide the navigation links/groups based on user role.

Refer to the example below:

```ts{3-4}
{
  path: '/acl',
  action: 'read',
  subject: 'acl-page',
  icon: 'mdi:shield-outline',
  title: 'Access Control'
}
```

## Home URL

You can find home URL based on user role in `src/layout/components/acl/getHomeRoute.tsx` file. Currently, we have set default URL for client and admin like following:

<code-group>
<code-block title="TSX" active>
```tsx
// Set Home URL based on User Roles
const getHomeRoute = (role: string) => {
  if (role === 'client') return '/acl'
  else return '/dashboards/analytics'
}

export default getHomeRoute
```
</code-block>

<code-block title="JSX">
```jsx
// Set Home URL based on User Roles
const getHomeRoute = role => {
  if (role === 'client') return '/acl'
  else return '/dashboards/analytics'
}

export default getHomeRoute
```
</code-block>
</code-group>

## How to remove ACL

It is quite easy to remove access control from the template.

1. Remove the `src/configs/acl.ts` file
2. Remove the `import type { ACLObj } from 'src/configs/acl'` import statement & `acl?: ACLObj` from `next.d.ts` file if `next.d.ts` file is present in your project.
3. Remove the `src/@core/components/auth/AclGuard.tsx` file

4. Remove the AclGuard wrapper & ACL related imports from `src/pages/_app.tsx` file.

    Change following code ***from***:

    ```tsx
    // Code before removing ACL Guard
    import { defaultACLObj } from 'src/configs/acl'
    import AclGuard from 'src/@core/components/auth/AclGuard'

    const aclAbilities = Component.acl ?? defaultACLObj

    <AclGuard aclAbilities={aclAbilities} guestGuard={guestGuard} authGuard={authGuard}>
      {getLayout(<Component {...pageProps} />)}
    </AclGuard>
    ```

    ***to***

    ``` tsx
    // Code after removing ACL Guard
   {getLayout(<Component {...pageProps} />)}
    ```

5. Remove the `acl` method from all the components.

    Component ***from***:

    ```tsx
    const Component = () => <h1>Component</h1>

    Component.acl = {
      action: 'read',
      subject: 'component'
    }

    export default Component
    ```

    ***to***

    ```tsx
    const Component = () => <h1>Component</h1>

    export default Component
    ```

6. Remove `action` & `subject` properties if defined in your navigation files.

    Navigation object ***from***:

    ```ts
    {
      path: '/acl',
      action: 'read',
      subject: 'acl-page',
      icon: 'mdi:shield-outline',
      title: 'Access Control'
    }
    ```

    ***to***

    ```ts
    {
      path: '/acl',
      icon: 'mdi:shield-outline',
      title: 'Access Control'
    }
    ```

7. If you want to remove the ACL while preserving auth, and redirect Home URL to any URL, please modify the `src/pages/index.tsx` file like the following and update your redirection URL:

    ```tsx
    import { useEffect } from 'react'
    import { useRouter } from 'next/router'
    import { useAuth } from 'src/hooks/useAuth'
    import Spinner from 'src/@core/components/spinner'

    const Home = () => {
      const auth = useAuth()
      const router = useRouter()

      useEffect(() => {
        if (auth.user && router.route === '/') {
          router.replace('/dashboards/analytics')
        }
      }, [auth.user, router])

      return <Spinner sx={{ height: '100%' }} />
    }

    export default Home
    ```

    OR

    Render your component in `src/pages/index.tsx` file for the Home page like following:

    ```tsx
    const Component = () => <h1>Component</h1>

    export default Component
    ```

8. Remove the `ability` & `ability.can` function in all the CanView files in `src/layouts/components/acl` folder.

    If you want to remove ACL functionality and preserve Auth then replace the following codes in respective files.

    <code-group>
    <code-block title="TSX" active>
    ```tsx
    // src/layouts/components/acl/CanViewNavGroup.tsx
    import { ReactNode } from 'react'
    import { useAuth } from 'src/hooks/useAuth'
    import { NavGroup } from 'src/@core/layouts/types'

    interface Props {
      navGroup?: NavGroup
      children: ReactNode
    }

    const CanViewNavGroup = (props: Props) => {
      const { children, navGroup } = props

      const auth = useAuth()

      if (auth.user || (navGroup && navGroup.auth === false)) {
        return <>{children}</>
      } else {
        return null
      }
    }

    export default CanViewNavGroup
    ```
    </code-block>

    <code-block title="JSX">
    ```jsx
    // src/layouts/components/acl/CanViewNavGroup.js
    import { useAuth } from 'src/hooks/useAuth'

    const CanViewNavGroup = props => {
      const { children, navGroup } = props

      const auth = useAuth()

      if (auth.user || (navGroup && navGroup.auth === false)) {
        return <>{children}</>
      } else {
        return null
      }
    }

    export default CanViewNavGroup
    ```
    </code-block>
    </code-group>

    <code-group>
    <code-block title="TSX" active>
    ```tsx
    // src/layouts/components/acl/CanViewNavLink.tsx
    import { ReactNode } from 'react'
    import { useAuth } from 'src/hooks/useAuth'
    import { NavLink } from 'src/@core/layouts/types'

    interface Props {
      navLink?: NavLink
      children: ReactNode
    }

    const CanViewNavLink = (props: Props) => {
      const { children, navLink } = props

      const auth = useAuth()

      if (auth.user || (navLink && navLink.auth === false)) {
        return <>{children}</>
      } else {
        return null
      }
    }

    export default CanViewNavLink
    ```
    </code-block>

    <code-block title="JSX">
    ```jsx
   // src/layouts/components/acl/CanViewNavLink.js
    import { useAuth } from 'src/hooks/useAuth'

   const CanViewNavLink = props => {
     const { children, navLink } = props

     const auth = useAuth()

     if (auth.user || (navLink && navLink.auth === false)) {
       return <>{children}</>
     } else {
      return null
     }
   }

    export default CanViewNavLink
    ```
    </code-block>
    </code-group>

    <code-group>
    <code-block title="TSX" active>
    ```tsx
    // src/layouts/components/acl/CanViewNavSectionTitle.tsx
    import { ReactNode } from 'react'
    import { useAuth } from 'src/hooks/useAuth'
    import { NavSectionTitle } from 'src/@core/layouts/types'

    interface Props {
      children: ReactNode
      navTitle?: NavSectionTitle
    }

    const CanViewNavSectionTitle = (props: Props) => {
      const { children, navTitle } = props
      const auth = useAuth()

      if (auth.user || (navTitle && navTitle.auth === false)) {
        return <>{children}</>
      } else {
        return null
      }
    }

    export default CanViewNavSectionTitle
    ```
    </code-block>

    <code-block title="JSX">
    ```jsx
    // src/layouts/components/acl/CanViewNavSectionTitle.js
    import { useAuth } from 'src/hooks/useAuth'

    const CanViewNavSectionTitle = (props: Props) => {
      const { children, navTitle } = props

      const auth = useAuth()

      if (auth.user || (navTitle && navTitle.auth === false)) {
        return <>{children}</>
      } else {
        return null
      }
    }

    export default CanViewNavSectionTitle
    ```
    </code-block>
    </code-group>

     Replace the following codes in respective files in order to remove both Auth and ACL functionality.

    <code-group>
    <code-block title="TSX" active>
    ```tsx
    // src/layouts/components/acl/CanViewNavGroup.tsx
    import { ReactNode } from 'react'

    interface Props {
      children: ReactNode
    }

    const CanViewNavGroup = (props: Props) => {
      const { children } = props

        return <>{children}</>
    }

    export default CanViewNavGroup
    ```
    </code-block>

    <code-block title="JSX">
    ```jsx
    // src/layouts/components/acl/CanViewNavGroup.js
    const CanViewNavGroup = props => {
      const { children } = props

      return <>{children}</>
    }

    export default CanViewNavGroup
    ```
    </code-block>
    </code-group>

    <code-group>
    <code-block title="TSX" active>
    ```tsx
    // src/layouts/components/acl/CanViewNavLink.tsx
    import { ReactNode } from 'react'

    interface Props {
      children: ReactNode
    }

    const CanViewNavLink = (props: Props) => {
      const { children } = props

      return <>{children}</>
    }

    export default CanViewNavLink
    ```
    </code-block>

    <code-block title="JSX">
    ```tsx
    // src/layouts/components/acl/CanViewNavLink.js
   const CanViewNavLink = props => {
     const { children } = props

      return <>{children}</>
   }

    export default CanViewNavLink
    ```
    </code-block>
    </code-group>

    <code-group>
    <code-block title="TSX" active>
    ```tsx
    // src/layouts/components/acl/CanViewNavSectionTitle.tsx
    import { ReactNode } from 'react'

    interface Props {
      children: ReactNode
    }

    const CanViewNavSectionTitle = (props: Props) => {
      const { children } = props

        return <>{children}</>
    }

    export default CanViewNavSectionTitle
    ```
    </code-block>

    <code-block title="JSX">
    ```jsx
    // src/layouts/components/acl/CanViewNavSectionTitle.js
    const CanViewNavSectionTitle = (props) => {
      const { children } = props

        return <>{children}</>
    }

    export default CanViewNavSectionTitle
    ```
    </code-block>
    </code-group>