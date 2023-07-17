---
sidebarDepth: 0
---

# How to change Mode [Light / Dark] ?

In Modern era most of the user prefer to work in dark mode due to eye strain and long working hours.

It's very easy to change the default mode to dark from the ThemeConfig. Please refer our Theme Configurations docs and set `mode` property from `light` to `dark`.

[Theme Configuration Doc](/guide/settings/theme-config.html)

There may be times where you would want to have both light & dark mode in your application and implement some functionalities or styling based on the current mode. To read the current mode please refer following docs:

[Read Current Mode for Conditional Styling Doc](/guide/settings/hooks.html#read-values-from-settings-context)

We already provide mode toggle in the Appbar(Navbar) but In case you want to implement mode toggler on your own or make changes in the mode toggler, please follow below documentation:

[Mode Toggler Doc](/guide/settings/hooks.html#update-single-value-in-settings-context)
