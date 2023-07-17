# How to add i18n routing

## Routing Synced With I18n

1. Open the `next.config.js` file and add the `i18` property with the languages you need

```js
i18n: {
  locales: ['en', 'fr', 'ar'],
  defaultLocale: 'en'
},
```

2. Create a `useEffect` in the `src/pages/_app.tsx` file to watch changes of i18n language and to preserve the language in case the page is reloaded:

```tsx
import { useEffect } from 'react'
import { useRouter } from 'next/router'
import { useTranslation } from 'react-i18next'

const App = () => {
  const router = useRouter()
  const { i18n } = useTranslation()
  const { locale } = router

  useEffect(() => {
    if (locale !== 'en') {
      i18n.changeLanguage(locale)
    }
  }, [locale])

  return (
    ...
  )
}

export default App
```

3. To switch a language, push the `locale` parameter with `router.push`:

<code-group>
<code-block title="TSX" active>
```tsx
import { useRouter } from 'next/router'
import { useTranslation } from 'react-i18next'

const Component = () => {
  const router = useRouter()
  const { i18n } = useTranslation()

  const handleLangChange = (lang: string) => {
    i18n.changeLanguage(lang)
    router.push(router.asPath, undefined, { locale: lang })
  }

  return (
    <div>
      <button onClick={() => handleLangChange('en')}>EN</button>
      <button onClick={() => handleLangChange('fr')}>FR</button>
      <button onClick={() => handleLangChange('ar')}>AR</button>
    </div>
  )
}

export default Component
```
</code-block>

<code-block title="JSX">
```jsx
import { useRouter } from 'next/router'
import { useTranslation } from 'react-i18next'

const Component = () => {
  const router = useRouter()
  const { i18n } = useTranslation()

  const handleLangChange = lang => {
    i18n.changeLanguage(lang)
    router.push(router.asPath, undefined, { locale: lang })
  }

  return (
    <div>
      <button onClick={() => handleLangChange('en')}>EN</button>
      <button onClick={() => handleLangChange('fr')}>FR</button>
      <button onClick={() => handleLangChange('ar')}>AR</button>
    </div>
  )
}

export default Component
```
</code-block>
</code-group>

4. Import `locale` from the `useRouter` hook and add the `locale` prop to every NextJS link that is used in your app:

```tsx
import Link from 'next/link'
import { useRouter } from 'next/router'

const Component = () => {
  const router = useRouter()
  const { locale } = router

  return <Link href='...' locale={locale}>text</Link>
}

export default Component
```

5. If you have `getStaticPaths` & `getStaticProps` in your component then you'll have to do the following otherwise you'll be redirected to `404`

```tsx
export const getStaticProps = ({ locale, locales }) => {
  return {
    props: {
      locale,
      locales,
    },
  }
}

export const getStaticPaths = ({ locales }) => {
  const paths = []

  for (const locale of locales) {
    paths.push({ params: { ... }, locale })
    paths.push({ params: { ... }, locale })
  }

  return {
    paths,
    fallback: true,
  }
}
```
