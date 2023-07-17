# How to add MUI localization

::: warning
To use MUI localization you'll have to make changes in the `ThemeComponent.tsx` file.

You'll have to make a copy of the `ThemeComponent.tsx` file to keep it as a backup while updating the template.
:::

## Localization Synced With I18n

1. Open the `src/@core/theme/ThemeComponent.tsx` file
2. Import the locales you need from `'@mui/material/locale'`

<code-group>
<code-block title="TS" active>
```tsx
import { arEG, enUS, frFR, Localization } from '@mui/material/locale'
```
</code-block>

<code-block title="JS">
```jsx
import { arEG, enUS, frFR } from '@mui/material/locale'
```
</code-block>
</code-group>

3. Import the `useTranslation` hook from `react-i18next`

```jsx
import { useTranslation } from 'react-i18next'
```

4. Create a `langObj` variable

<code-group>
<code-block title="TS" active>
```tsx
const langObj: { [key: string]: Localization } = {
  fr: frFR,
  ar: arEG,
  en: enUS
}
```
</code-block>

<code-block title="JS">
```jsx
const langObj = {
  fr: frFR,
  ar: arEG,
  en: enUS
}
```
</code-block>
</code-group>

5. Initialize the `useTranslation` hook

```jsx
const { i18n } = useTranslation()
```

6. Add the language as a parameter to the `createTheme` function

```jsx
theme = createTheme(
  theme,
  {
    components: { ...mergeComponentOverrides(theme, settings) },
    typography: { ...mergeTypography(theme) }
  },
  langObj[i18n.language]
  )
```
