---
sidebarDepth: 0
---

# How to use Nextjs Image Component without Height & Width ?

There might be a time where you'll have to use an image without height or width. But, the Nextjs Image component
requires both height & width.

In that case, you can do something like this:

```tsx
<Box sx={{ width: 35, height: 35 }}>
  <Img width='100%' height='100%' layout='responsive' objectFit='contain' src='/images/logos/facebook.png' />
</Box>
```
