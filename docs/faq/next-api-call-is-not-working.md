---
sidebarDepth: 0
---

# Why Next.js API call is not working

It is possible that API calls from the `pages/api/*` folder may not function as intended. This issue arises due to a compatibility issue between the latest version of Axios and the mock adapter (`axios-mock-adapter`).

To rectify the issue, either downgrading Axios to version `v1.1.0` or utilizing the [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) (`fetch()`) would provide a resolution.
