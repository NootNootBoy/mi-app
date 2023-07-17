---
sidebarDepth: 0
---

# Installation warnings

You might get some warnings while running `yarn install` or `npm install` like below:

<img alt='installation warnings' class='medium-zoom' :src="$withBase('/images/faqs/installation-warnings.png')" />

The warnings you are receiving while installing is from library/packages we use.

We always keep our packages up to date when we make a major release. However, the writer of that package may have used an older dependency that is no longer maintained for backward compatibility or any other code related issue. But, that's not an issue. Those packages will work fine with our template.

**Also, check if you're missing files staring with a dot(.eslintrc.json)**

Even if you like to try, you can install this packages in fresh React project without our template and you will get the same.
