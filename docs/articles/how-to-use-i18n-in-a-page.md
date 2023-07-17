# How to use i18n in a page

Sneat admin provides i18n for navigation only. There might be a time when you might want to translate any text in a page. Here's how you can achieve that:

1. Make sure your have `i18next`, `react-i18next`, `i18next-http-backend` and `i18next-browser-languagedetector` packages installed
2. Copy the `src/configs/i18n.ts` file from the full version and paste it under the same directory in your project
3. Add `import 'src/configs/i18n'` import statement in the `src/pages/_app.tsx` file
4. Create a `locales` folder in the `public` folder
5. Create JSON files with language as their file names in `locales` depending on the languages you need. For example, we're using three languages English, French & Arabic

```json
// en.json
{
  "Hello World": "Hello World"
}
```

```json
// fr.json
{
  "Hello World": "Bonjour le monde"
}
```

```json
// ar.json
{
  "Hello World": "مرحبا بالعالم"
}
```

6. Import `useTranslation` in the page where you want to translate the content

```tsx
import { useTranslation } from 'react-i18next'
```

7. You can now initialize the `useTranslation` and use the `changeLanguage` function to change the language

```tsx
import { useTranslation } from 'react-i18next'

const Component = () => {
  const { t, i18n } = useTranslation()

  return (
    <div>
      <h1>{t('Hello World')}</h1>
      <button onClick={() => i18n.changeLanguage('fr')}>Translate</button>
    </div>
  )
}

export default Component
```
