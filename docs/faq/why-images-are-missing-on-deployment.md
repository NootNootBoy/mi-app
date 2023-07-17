---
sidebarDepth: 0
---

# Why images are missing on deployment ?

The reason behind the missing images on deployment is may be that you are deploying the project in a sub-folder. In this case, please consider following this [article](https://nextjs.org/docs/api-reference/next.config.js/basepath#images) suggested by NextJS.

Let's consider you are deploying your project under docs folder. So your `basePath` will look like `basePath: '/docs'` and you will need to add the `basePath` in front of `src`.

For example, using `/docs/me.png` will properly serve your image when `basePath` is set to `/docs`.

When using `next/image` consider following:

```tsx
import Image from 'next/image'

function Home() {
  return (
    <>
      <h1>My Homepage</h1>
      <Image src='/docs/me.png' alt='Picture of the author' width={500} height={500} />
      <p>Welcome to my homepage!</p>
    </>
  )
}

export default Home
```

When using `<img>` tag to serve images consider following:

```tsx
function Home() {
  return (
    <>
      <h1>My Homepage</h1>
      <img src='/docs/me.png' alt='Picture of the author' />
      <p>Welcome to my homepage!</p>
    </>
  )
}

export default Home
```
