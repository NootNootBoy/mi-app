# Internationalization (i18n)

## Overview

We're using [react-i18next](https://react.i18next.com/) for Internationalization. You can find its configurations in `src/configs/i18n.ts` file and the locales in `public/locales` folder in the full version.

## Usage

Refer to [this article](/articles/how-to-use-i18n-in-a-page.html) to implement the internationalization.

## Add i18n

::: warning
Only for those who are using the starter-kit
:::

If you are using the full version, then you don't need to add i18n as it is already available in that version. But if you are using the starter-kit (which is recommended) and want to add i18n, then follow these steps:

- You need to add these npm packages:
  - `i18next`
  - `react-i18next`
  - `i18next-http-backend`
  - `i18next-browser-languagedetector`

<code-group>
<code-block title="YARN (Highly Recommended)" active>
```bash
yarn add i18next react-i18next i18next-http-backend i18next-browser-languagedetector
```
</code-block>

<code-block title="NPM">
```bash
npm install i18next react-i18next i18next-http-backend i18next-browser-languagedetector
```
</code-block>
</code-group>

- Copy `src/configs/i18n.ts` file from the full version and paste it under the same directory in your project
- Add `import 'src/configs/i18n'` import statement in `src/pages/_app.tsx` file
- Add your locale files in `public/locales` folder
- If you want to translate the navigation menu, then copy the whole code from `src/layouts/components/Translations.tsx` file from the full version and paste it under the same directory in your project
- If you want a language dropdown in the appBar to change the current language in the app, then import `src/@core/layouts/components/shared-components/LanguageDropdown.tsx` file and render `LanguageDropdown` component in `src/layouts/components/vertical/AppBarContent.tsx` or `src/layouts/components/horizontal/AppBarContent.tsx` file

```tsx
<LanguageDropdown settings={settings} saveSettings={saveSettings} />
```

## Remove i18n

::: warning
Only for those who are using the full version
:::

If you do not want to use i18n, we recommend you start your project with the starter-kit. But if you are using the full version and does not want to use i18n, then follow these steps:

- You may remove all the packages related to i18n from `package.json` file if you want to
  - `i18next`
  - `react-i18next`
  - `i18next-http-backend`
  - `i18next-browser-languagedetector`
- Remove `src/configs/i18n.ts` file
- Remove `import 'src/configs/i18n'` import statement from `src/pages/_app.tsx` file
- Replace the following code in `src/layouts/components/Translations.tsx` file

<code-group>
<code-block title="TSX" active>
```tsx{5}
interface Props {
  text: string
}

const Translations = ({ text }: Props) => <>{text}</>

export default Translations
```
</code-block>

<code-block title="JSX">
```jsx{1}
const Translations = ({ text }) => <>{text}</>

export default Translations
```
</code-block>
</code-group>

- Remove `LanguageDropdown` file import statement and rendered component from `src/layouts/components/vertical/AppBarContent.tsx` and/or `src/layouts/components/horizontal/AppBarContent.tsx` file

```tsx
<LanguageDropdown settings={settings} saveSettings={saveSettings} />
```

- Remove your locale files from `public/locales` folder

## Add / Remove a language

Suppose you want to add `de` (German) language and remove `ar` (Arabic) language. For this, you need to follow these steps:

- Remove `public/locales/ar.json` file and add `public/locales/de.json` file. You need to keep the format of the file as it is in other locale files
- Make a new file in `src/layouts/components` folder and place the following code in this file

<code-group>
<code-block title="TSX" active>
```tsx
// src/layouts/components/UserLanguageDropdown.tsx

import { Fragment, SyntheticEvent, useState } from 'react'
import Menu from '@mui/material/Menu'
import MenuItem from '@mui/material/MenuItem'
import IconButton from '@mui/material/IconButton'
import { useTranslation } from 'react-i18next'
import Icon from 'src/@core/components/icon'
import { Settings } from 'src/@core/context/settingsContext'

interface Props {
  settings: Settings
}

const UserLanguageDropdown = ({ settings }: Props) => {
  // ** State
  const [anchorEl, setAnchorEl] = useState<any>(null)

  // ** Hook
  const { i18n } = useTranslation()

  // ** Var
  const { layout } = settings

  const handleLangDropdownOpen = (event: SyntheticEvent) => {
    setAnchorEl(event.currentTarget)
  }
  const handleLangDropdownClose = () => {
    setAnchorEl(null)
  }
  const handleLangItemClick = (lang: 'en' | 'fr' | 'de') => {
    i18n.changeLanguage(lang)
    handleLangDropdownClose()
  }

  return (
    <Fragment>
      <IconButton
        color='inherit'
        aria-haspopup='true'
        aria-controls='customized-menu'
        onClick={handleLangDropdownOpen}
        sx={layout === 'vertical' ? { mr: 0.75 } : { mx: 0.75 }}
      >
        <Icon icon='mdi:translate' />
      </IconButton>
      <Menu
        anchorEl={anchorEl}
        open={Boolean(anchorEl)}
        onClose={handleLangDropdownClose}
        sx={{ '& .MuiMenu-paper': { mt: 4, minWidth: 130 } }}
        anchorOrigin={{ vertical: 'bottom', horizontal: 'right' }}
        transformOrigin={{ vertical: 'top', horizontal: 'right' }}
      >
        <MenuItem sx={{ py: 2 }} selected={i18n.language === 'en'} onClick={() => handleLangItemClick('en')}>
          English
        </MenuItem>
        <MenuItem sx={{ py: 2 }} selected={i18n.language === 'fr'} onClick={() => handleLangItemClick('fr')}>
          French
        </MenuItem>
        <MenuItem sx={{ py: 2 }} selected={i18n.language === 'de'} onClick={() => handleLangItemClick('de')}>
          German
        </MenuItem>
      </Menu>
    </Fragment>
  )
}

export default UserLanguageDropdown
```
</code-block>

<code-block title="JSX">
```jsx
// src/layouts/components/UserLanguageDropdown.js

import { Fragment, useState } from 'react'
import Menu from '@mui/material/Menu'
import MenuItem from '@mui/material/MenuItem'
import IconButton from '@mui/material/IconButton'
import { useTranslation } from 'react-i18next'
import Icon from 'src/@core/components/icon'

const UserLanguageDropdown = ({ settings }) => {
  // ** State
  const [anchorEl, setAnchorEl] = useState(null)

  // ** Hook
  const { i18n } = useTranslation()

  // ** Var
  const { layout } = settings

  const handleLangDropdownOpen = event => {
    setAnchorEl(event.currentTarget)
  }
  const handleLangDropdownClose = () => {
    setAnchorEl(null)
  }
  const handleLangItemClick = lang => {
    i18n.changeLanguage(lang)
    handleLangDropdownClose()
  }

  return (
    <Fragment>
      <IconButton
        color='inherit'
        aria-haspopup='true'
        aria-controls='customized-menu'
        onClick={handleLangDropdownOpen}
        sx={layout === 'vertical' ? { mr: 0.75 } : { mx: 0.75 }}
      >
        <Icon icon='mdi:translate' />
      </IconButton>
      <Menu
        anchorEl={anchorEl}
        open={Boolean(anchorEl)}
        onClose={handleLangDropdownClose}
        sx={{ '& .MuiMenu-paper': { mt: 4, minWidth: 130 } }}
        anchorOrigin={{ vertical: 'bottom', horizontal: 'right' }}
        transformOrigin={{ vertical: 'top', horizontal: 'right' }}
      >
        <MenuItem sx={{ py: 2 }} selected={i18n.language === 'en'} onClick={() => handleLangItemClick('en')}>
          English
        </MenuItem>
        <MenuItem sx={{ py: 2 }} selected={i18n.language === 'fr'} onClick={() => handleLangItemClick('fr')}>
          French
        </MenuItem>
        <MenuItem sx={{ py: 2 }} selected={i18n.language === 'de'} onClick={() => handleLangItemClick('de')}>
          German
        </MenuItem>
      </Menu>
    </Fragment>
  )
}

export default UserLanguageDropdown
```
</code-block>
</code-group>

- Import the `src/layouts/components/UserLanguageDropdown.tsx` file and render it in the `src/layouts/components/vertical/AppBarContent.tsx` and/or `src/layouts/components/horizontal/AppBarContent.tsx` file.

<code-group>
<code-block title="TSX" active>
```tsx{6,23}
// src/layouts/components/vertical/AppBarContent.tsx
// OR
// src/layouts/components/horizontal/AppBarContent.tsx

import { Settings } from 'src/@core/context/settingsContext'
import UserLanguageDropdown from 'src/layouts/components/UserLanguageDropdown'

interface Props {
  hidden: boolean
  settings: Settings
  toggleNavVisibility: () => void // in src/layouts/components/vertical/AppBarContent.tsx file only
  saveSettings: (values: Settings) => void
}

const AppBarContent = (props: Props) => {
  // in src/layouts/components/horizontal/AppBarContent.tsx file,
  // toggleNavVisibility prop will not come in the next line
  const { hidden, settings, saveSettings, toggleNavVisibility } = props

  return (
    <>
      {/* Your some content */}
      <UserLanguageDropdown settings={settings} />
    </>
  )
}

export default AppBarContent
```
</code-block>

<code-block title="JSX">
```jsx{5,15}
// src/layouts/components/vertical/AppBarContent.js
// OR
// src/layouts/components/horizontal/AppBarContent.js

import UserLanguageDropdown from 'src/layouts/components/UserLanguageDropdown'

const AppBarContent = props => {
  // in src/layouts/components/horizontal/AppBarContent.js file,
  // toggleNavVisibility prop will not come in the next line
  const { hidden, settings, saveSettings, toggleNavVisibility } = props

  return (
    <>
      {/* Your some content */}
      <UserLanguageDropdown settings={settings} />
    </>
  )
}

export default AppBarContent
```
</code-block>
</code-group>
