# Page Specific Settings

If you want to override specific settings for specific page only, you can do that as well.

## Usage

To change a setting for a specific page, use `setConfig` method and return an object with your settings like below:

```tsx
const AnalyticsDashboard = () => <h1>Analytics Dashboard</h1>

AnalyticsDashboard.setConfig = () => {
  return {
    mode: 'dark'
    ...
  }
}

export default AnalyticsDashboard
```

::: tip Note
You can override any config property at page level. Please refer [Theme Configurations](/guide/settings/theme-config.html) doc for each configurable property.
:::

::: danger Important
It is not advisable to override `layout` or `rtl`  property for a specific page, they should be set only globally. Overriding them at page level will throw a memory leak error.
:::
