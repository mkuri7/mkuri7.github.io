# Gutenberg Block Development File Structure

## Overview

Modern Gutenberg blocks follow a standardized file structure. Although not every file is required, most block projects are organized like this:

```text
my-block/
├── block.json
├── edit.js
├── save.js
├── render.php
├── index.js
├── editor.scss
├── style.scss
└── view.js
```

Depending on whether the block is **Static** or **Dynamic**, some files may not be used.

---

# File Responsibilities

## block.json

### Purpose

The blueprint of the block.

This file defines the block's metadata, attributes, default values, icons, category, scripts, styles, and other configuration.

### Typical Responsibilities

- Block name
- Title
- Category
- Icon
- Attributes
- Default values
- Editor script
- Frontend script
- Styles

### Example

```json
{
    "attributes": {
        "title": {
            "type": "string",
            "default": "Masao's Lab"
        }
    }
}
```

Think of **block.json** as the single source of truth for the block.

---

## edit.js

### Purpose

Defines how the block behaves inside the WordPress Editor.

This is a React component that provides the editing experience.

### Typical Responsibilities

- RichText
- TextControl
- InspectorControls
- MediaUpload
- Buttons
- React state
- User interaction

### Runs In

- WordPress Block Editor only

Think of **edit.js** as the editor UI.

---

## render.php

### Purpose

Generates the HTML shown on the public website.

Unlike edit.js, this file runs on the server using PHP.

### Typical Responsibilities

- Generate HTML
- Escape output
- Display attributes
- Server-side rendering

### Runs In

- Frontend
- Public website

Think of **render.php** as the frontend renderer.

---

## save.js

### Purpose

Used by Static Blocks.

Returns the HTML that will be stored inside the post content.

### Note

Dynamic Blocks do **not** use save.js.

Instead, they use render.php.

---

## index.js

### Purpose

Registers the block with WordPress.

This file connects block.json with the React editor component.

### Typical Responsibilities

- registerBlockType()
- Import edit.js
- Import styles

Think of **index.js** as the entry point.

---

## style.scss

### Purpose

Shared styles.

These styles are loaded in both:

- Editor
- Frontend

Use this file for styles that should appear everywhere.

---

## editor.scss

### Purpose

Editor-only styles.

These styles are loaded only inside the Gutenberg editor.

Typical uses include:

- Editor outlines
- Helper borders
- Placeholder styling
- Editor layout adjustments

---

## view.js

### Purpose

Frontend JavaScript.

Used when the block needs interactive behavior after the page is loaded.

Typical uses include:

- Button click handling
- Ajax requests
- Animations
- Dynamic UI
- API calls

---

# Static Block vs Dynamic Block

## Static Block

```text
Editor
    ↓
save.js
    ↓
HTML stored in post
    ↓
Frontend
```

HTML is generated when the post is saved.

---

## Dynamic Block

```text
Editor
    ↓
Attributes
    ↓
render.php
    ↓
HTML generated on each page request
```

HTML is generated every time the page is viewed.

---

# Typical Dynamic Block Structure

```text
alfred-affiliate/
├── block.json      ← Blueprint
├── edit.js         ← React Editor
├── render.php      ← Frontend Renderer
├── index.js        ← Entry Point
├── editor.scss     ← Editor Styles
├── style.scss      ← Shared Styles
└── view.js         ← Frontend JavaScript (optional)
```

---

# Quick Summary

| File | Purpose |
|------|---------|
| block.json | Block blueprint and metadata |
| edit.js | React editor UI |
| render.php | Frontend HTML generation (Dynamic Block) |
| save.js | HTML generation (Static Block) |
| index.js | Block registration |
| style.scss | Shared styles |
| editor.scss | Editor-only styles |
| view.js | Frontend JavaScript |

---

# Simple Mental Model

```text
block.json
      │
      ├───────────────┐
      │               │
      ▼               ▼
edit.js         render.php
(Editor)        (Frontend)
      ▲               ▲
      └──── index.js ─┘
```

If you remember only one thing:

- **block.json** = Blueprint
- **edit.js** = Editor
- **render.php** = Frontend
- **index.js** = Entry Point
