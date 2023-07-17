---
sidebarDepth: 0
---

# React Draft Wysiwyg

## Overview

You may visit [React Draft Wysiwyg Docs](https://jpuri.github.io/react-draft-wysiwyg/#/docs) for a proper explanation of how to use it.

We have created a wrapper that dynamically returns the editor component from the `react-draft-wysiwyg` package so that you don't have to do it manually all the time you use it.

## Usage

You can create your editor as it is in the [React Draft Wysiwyg Docs](https://jpuri.github.io/react-draft-wysiwyg/#/docs) but make sure that you do not import the `react-draft-wysiwyg` package but instead add `import ReactDraftWysiwyg from 'src/@core/components/react-draft-wysiwyg'` import statement.

Let us take a look:

```tsx
import ReactDraftWysiwyg from 'src/@core/components/react-draft-wysiwyg'

const Editor = () => <ReactDraftWysiwyg />

export default Editor
```
