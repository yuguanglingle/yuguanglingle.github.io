# yuguanglingle.github.io

My personal site. Push to `main`, GitHub rebuilds it in a minute or two.

## What's here

```
index.html          my intro + the list of articles   <- edit this to change the intro
articles/           one file per article
articles/images/    screenshots and pictures
style.css           how everything looks
_layouts/article.html   the frame drawn around every article
```

That's all of it. There is nothing else to understand.

## Write an article

Create `articles/my-title.md`:

```markdown
---
layout: article
title: "My title"
date: 2026-09-01
---

Write in normal Markdown. Headings, lists, `code`, > quotes, links, tables all work.
```

It appears at `/articles/my-title.html` and shows up on the home page automatically —
the list sorts itself by `date`. The three lines of front matter are the only rule:
without them the file won't become a page.

Need raw HTML instead — a chart, a diagram, an embedded demo? Name the file `.html`,
keep the same front matter, and write HTML in the body. See
`articles/an-article-written-in-html.html`.

## Pictures

Drop the file in `articles/images/`, then in Markdown:

```markdown
![What it shows](/articles/images/my-screenshot.png)
```

## Preview it locally (optional)

Not required — you can just push and look at the live site. If you want it locally:

```bash
gem install bundler jekyll
jekyll serve
```

Then open http://localhost:4000.
