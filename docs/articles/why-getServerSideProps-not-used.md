# getServerSideProps method

## What is getServerSideProps?

Please refer to [this](https://nextjs.org/docs/basic-features/data-fetching/get-server-side-props) Next.js docs for the details on the `getServerSideProps` method.

## How to use getServerSideProps?

Please refer to [this](https://nextjs.org/docs/api-reference/data-fetching/get-server-side-props) Next.js docs to know how to use the `getServerSideProps` method.

## Why have we not used the getServerSideProps method?

We are using `@fake-db`; thus, we weren't bound to use the `getServerSideProps` method.

::: warning NOTE
If you are using the `getServerSideProps` method and exporting the static HTML files to your server, [these](https://nextjs.org/docs/advanced-features/static-html-export#unsupported-features) are unsupported features that cannot be computed during the build process.
:::
