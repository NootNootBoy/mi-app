---
sidebarDepth: 0
---

# Installation errors

Causes of `yarn install` or `npm install` issues can be due to various things which include:

- Missing or inappropriate dependencies like node or some other environmental issues
- Dependency resolved by package manager (yarn/npm) conflicts with other installed dependency
- The dependency of the package we use have an internal issue or that dependency has some issue with your environment
- Package or dependency of the package requires some additional step or configuration to work in your environment
- Downloaded package is broken or is tampered with.

To resolve such installation issues:

- Try using yarn if possible (recommended)
- Please try downloading the fresh package/zip and performing the installation again
- Please make sure you are using the LTS version of node which is recommended and not one with the latest features
- Try running the `yarn cache clean` or `npm cache clean` command.

After following the steps explained above, if you are still getting any errors, please [raise support](/guide/overview/support.md) at our support portal with the below details:

- Your OS information, Node version, yarn/npm version, Template/Package version
- Mention if you can run a fresh react project using `create-next-app` without our template
- Attach log file of the error you are getting in your console (provide full log)
- Mention which command you are running
- Mention if you were able to run our template on one machine and not on another.
