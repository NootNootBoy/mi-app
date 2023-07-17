# Folder Structure

::: danger Heads Up
Do not make any changes in the `src/@core` folder unless suggested by our support team. It is the core functionality of the template which is responsible to run the template and will be updated with every new update. Use `src/layouts` folder to override core layouts and components.
:::

Understand folder structure of the template and what every folder contains.

## Overview

Before checking folder structure it is better you know some stuff related to folder structure.

- `src/@core` folder contains core files of template which **shall not get modified** unless our support team guide you to do it.
- Outside of `src/@core` folder are files you can move and modify as per your wish. Basically that is your playground where you can modify anything.
- `src/@fake-db` folder just contains dummy data which we get in response of API call. This enables us to take step forward in providing **API ready template**.
- `src/layouts` folder outside of `src/@core` are your layouts which you can modify however you like. Template will always render these layouts.

## Main Package

Following is the folder structure of the full-version under both typescript / javascript version. Not explaining the folder structure for starter kit as everything is covered in the full version.

```
├── public
│   ├── images                   -> Static assets
│   ├── locales                  -> Translations
│   └── other files
├── src
│   ├── @core                    -> Template's core files
│   ├── @fake-db                 -> Fake Database for mocking axios requests (Fake API Calls)
│   ├── configs                  -> Configuration files
│   │   ├── acl.ts               -> Your Access Control file/configurations
│   │   ├── auth.ts              -> Your authentication file/configurations
│   │   ├── i18n.ts              -> i18n configurations and initialization
│   │   └── themeConfig.ts       -> Template configurations
│   ├── context                  -> Your context files go here
│   ├── hooks                    -> Your hooks go here
│   ├── layouts                  -> Your layouts
│   │   ├── components           -> Your components, layout components
│   │   ├── UserLayout.tsx       -> File responsible to render layout & template
│   │   └── UserThemeOptions.ts  -> Your theming file to override core theming
│   ├── navigation               -> Vertical & Horizontal static navigation menu files
│   │   ├── horizontal
│   │   └── vertical
│   ├── pages                    -> View files that render all the pages
│   │   ├── _app.tsx             -> Main file responsible to render layout
│   │   ├── _document.tsx        -> HTML document & emotions configurations
│   │   └── index.tsx            -> Application entry file
│   ├── store                    -> Redux store
│   ├── types                    -> All types (only in the typescript version)
│   └── views                    -> View files that are included in pages folder
├── styles                       -> Global styling
├── .env                         -> Environment file
├── .eslintrc.json               -> ESLint configurations (Linting code)
├── .gitignore                   -> gitignore (ignore files and folder to sync with repo)
├── .npmrc                       -> Node configuration file
├── .nvmrc                       -> nvm configuration file
├── .prettierrc.js               -> Prettier configurations (editor code formatting)
├── next.config.js               -> Next js configurations
├── next.d.ts                    -> Next js global types configurations
├── package.json                 -> All the dependencies require to run the template
├── tsconfig.json               -> TypeScript configurations
```

## @core folder

`src/@core` folder is the core of our template which contains core layouts, components and theming where you should not make any change but override them with the help of our layout docs in case of any changes required in core files.

**`src/@core` folder isn't meant to get modified.** When you will update our template replacing this `src/@core` folder will hopefully update the template with minimum changes.

It's a good idea to have a look at it and know what it contains to use stuff we already invented so **you don't have to reinvent the wheel**.

### Understanding Core folder

Understanding the `src/@core` folder will save your development time and you will know how to get most out of our template.

| Folder     | Description                                                                                                                                   |
| :--------- | :-------------------------------------------------------------------------------------------------------------------------------------------- |
| components | It contains core components of the template. Make sure to check them all in our custom components section                                     |
| context    | Settings context which is responsible for live template customization                                                                         |
| hooks      | useSettings is used to access settings context values, useBgColor is used to get different colors and useClipboard is used to copy some texts |
| layouts    | All the layouts and layout components like menu, appBar and footer reside in this folder for any user to override from the @core folder       |
| styles     | MUI's stepper styled component and all the third party styled components reside in this folder                                                |
| theme      | All the MUI theming like palette, breakpoints, typography, component's styling etc. are done in this folder                                   |
| utils      | All the helpful functions used in whole template. Users can also import and use these useful functions.                                       |
