---
title: Markdown Cheatsheet
slug: markdown-cheatsheet
excerpt: Examples of the most common markdown syntax. Used the following xharacters to add things like headings, lists, links, images, emojis, horizontal rules, and more.
date: 2022-11-09
author: Jim Kernix
---

## Markdown Syntax

Here are some of the most common ways to add styling to your markdown posts.

## Headings

Use a hash tag for headings

```md
# Single hash for h1 tag
## Two hash tags for h2
### Two for h2 tag, etc. up to h6
```

## Links

Use the following syntax to add links to your posts. For more markdown syntax check out my GitHub repository [Markdown Cheatsheet](https://github.com/Kernix13/markdown-cheatsheet). But the basic syntax is the link text goes inside square brackets `[]`, followed by the URL in parentheses `()`.

```md
[Markdown Cheatsheet](https://github.com/Kernix13/markdown-cheatsheet)
```

## Formatting

Text can be formatted as **bold**, _italic_, and/or ~~strikethrough~~ using markdown syntax. You can also use the HTML tag `<ins>` to <ins>underline</ins> text. 

### Bold text 

Bold text is used by surrounding the text with 2 asterisk characters (`**`):

```md
**Bold text**
```

### Italic text 

Italic text is used by surrounding the text with 1 asterisk character (`*`) or 1 underscore character (`_`):

```md
*Italic text*
_Italic text_
```

### Strikethrough text 

Strikethrough text is used by surrounding the text with 2 tilde characters (`~~`):

```md
~~Strikethrough text~~
```

### Underlined text 

Underlined text is used by surrounding the text with the HTML `<ins>` tag:

```md
<ins>Underlined text</ins>
```

## Blockquotes

> Something here

## Horizontal rules

Something here

- - - 

## Lists

It appears Astro has some default styling for some of items on this page but it looks like you have to create your own CSS rules.

1. one
2. two
3. three
   1. nested item

## Code blocks

```js
const varName = [];

function fxName(param) {
  console.log("This is a javascript code block");
  return param;
}
```

## Images

Image goes here

## Emojis

Emojis here (not displaying?): :+1: | :heavy_check_mark: | :x: | :one: | 

## HTML Entities

Something here: &copy; | &check; | &#9998; | &#9986; | &uarr; | &#9650; | 