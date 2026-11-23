# personalwebsite-blogcontent

The content of the blog of [lukeneedham.com](https://lukeneedham.com): every article and every image
they use. The site's code is in [PersonalWebsite](https://github.com/LukeNeedham/PersonalWebsite),
which downloads this repo's `main` every time it is built.

The blog articles are just markdown files in git. They can be edited directly as the files via git, or they can be edited
via [Pages CMS](https://pagescms.org).

## Layout

```
articles/   one markdown file per article; the file name is the article's id (and its address)
images/     the images the articles use
```

## An article

```
---
title: My Article
image: my-article.png
date: 2026-09-12
---
The first paragraph has no heading, and `##` starts a section.
```

The page shows the title and date itself, so they are not repeated in the text. The date is `YYYY-MM-DD`. `image` is the
thumbnail shown in the list: the name of a file in `images/`.

An image goes in `images/`, and an article shows it with a path relative to the article, so it shows on GitHub too:

```
![The plan of the house](../images/house-plan.png)
```

## Publishing

A push to `main` publishes: a workflow checks the articles with the site's own build step, then asks Vercel to
rebuild the site. If an article is wrong (a missing field, a bad date) the check fails and says which, and the
live site stays as it was.

The workflow needs the repo secret `VERCEL_DEPLOY_HOOK_URL`: a Deploy Hook of the site's Vercel project
(Project Settings, Git, Deploy Hooks, on the `main` branch).

## Editing in a browser

[Pages CMS](https://pagescms.org) ([source](https://github.com/pages-cms/pages-cms), [docs](https://pagescms.org/docs/)) is a free,
open-source web editor for the files of a GitHub repo. [`.pages.yml`](.pages.yml) describes the articles to it. Sign in at
[app.pagescms.org](https://app.pagescms.org) and install its GitHub App on this repo. Someone without a GitHub account can
be invited by email as a collaborator of the repo in Pages CMS. Every save is a commit to `main`, which publishes.

## Previewing an article locally

Check out [PersonalWebsite](https://github.com/LukeNeedham/PersonalWebsite), then:

```
BLOG_CONTENT_DIR=/path/to/personalwebsite-blogcontent yarn dev
```

With `yarn dev` running, run the same with `yarn generate` after changing an article.
