---
layout: page
title: Special Characters in GitHub Pages
categories: [article, github, github_pages]
project: this_site
---

I found a few things challenging while working with [GitHub Pages], particularly dealing with formatting of the title. Because the title is used to reference the page, and my lists are dynamic, I want to be able to display subjects clearly, and not compromise because of limitations.

## Superscript and Subscript

The html tags `<sup>` and `<sub>` do not appear to work wtih Markdown... specifically with GitHub Pages. After some experimentation I found that I can create a span with a specific class and use css to format that span as superscript or subscript.

Here is how I implemented it: `E = MC<span class="sup">2</span>`, and here is what it looks like: E = MC<span class="sup">2</span>. The css is very straight forward.

```css
.sup {
    vertical-align: super;
}

.sub {
    vertical-align: sub;
}
```

## Showing a colon (:) in the title

Another issue that I had is that within the header section a colon is a special character. The qucik and easy fix for this is to use the encoded html tag `&#58;`.

[GitHub Pages]: https://pages.github.com/