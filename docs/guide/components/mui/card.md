---
sidebarDepth: 0
---

# Card

Please visit [MUI Card Docs](https://mui.com/material-ui/react-card/) for a proper explanation of the `Card` component.

## How to use Text Button inside Card Actions

If you are using a text button inside the `CardActions` component, you need to add the `.card-action-dense` class along with the `CardActions` component; otherwise, it will break the alignment.

- Without the `.card-action-dense` class

<img alt='card-actions-with-no-class' class='medium-zoom' :src="$withBase('/images/components/card-actions-with-no-class.png')" />

- With the `.card-action-dense` class

<img alt='card-actions-with-class' class='medium-zoom' :src="$withBase('/images/components/card-actions-with-class.png')" />

Here is the example of how to use the class mentioned above:

```tsx{3}
<Card>
  <CardContent>...</CardContent>
  <CardActions className='card-action-dense'>
    <Button variant='text'>Button</Button>
  </CardActions>
</Card>
```
