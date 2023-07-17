# Installation

Sneat is built using [Create Next App](https://nextjs.org/docs/getting-started). Create Next App sets up everything automatically for you.

## Guide

First of all make sure you have installed [Node](https://nodejs.org/en/) and [npm](https://www.npmjs.com/) / [yarn](https://yarnpkg.com/)

::: tip
Yarn package manager is recommended
:::

::: danger Requirements
Please make sure you use the node’s LTS version which is recommended by the official node site and not the one with the latest features or previous versions. Our project is not tested to work with other Node versions.
:::

::: danger Important!
Before installing the **node_modules**, make sure you have files starting with a **dot(.eslintrc, .env etc..)**. It mostly happens when hidden files are not enabled on your machine and you try to copy our template at some other place on your system.
:::

- After downloading zip, copy this zip to your desired location and then unzip it. **Do not unzip first and then copy files to another location**, it may not be able to run the template due to missing hidden files not copied over.
  
- In the uncompressed folder, you will find the `typescript-version` and `javascript-version` folders which contains the `full-version` & `starter-kit` folders. Open the one you want to get started with in your code editor.

- Run below command in console:

<code-group>
<code-block title="YARN (Highly Recommended)" active>
```bash
yarn install
```
</code-block>

<code-block title="NPM">
```bash
npm install
```
</code-block>
</code-group>

- After installing the modules run your project with following command:

<code-group>
<code-block title="YARN (Highly Recommended)" active>
```bash
yarn dev
```
</code-block>

<code-block title="NPM">
```bash
npm run dev
```
</code-block>
</code-group>

- You will find following output after running above command in console:
  
<img class='rounded medium-zoom' alt='console-output-of-development-server' :src="$withBase('/images/development/server-console.png')" />

- Congratulations!! You have successfully run the project. Visit [http://localhost:3000/](http://localhost:3000/) to check it in your browser.

::: tip NOTE
Your network URL might not have same URL as screenshot and that is completely fine. It depends on your network.
:::
