---
name: update-github-info
description: Refresh the GitHub Info page with practical, sourced updates from the GitHub Blog and Changelog.
intent: Keep Mona's GitHub Info page useful to developers by proposing concise, accurate updates based on recent official GitHub news.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
strict: true
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - github.blog
    - github.com
tools:
  edit: true
  web-fetch: {}
safe-outputs:
  noop:
  create-pull-request:
    title-prefix: "Update GitHub Info: "
    base-branch: main
    draft: false
    reviewers:
      - mona
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and `site/content/github-info.md`. Fetch both
https://github.blog/latest/ and https://github.blog/changelog/ with the web-fetch
tool. Use only details and source links verified on those pages.

Select recent items that offer practical guidance for developers and fit the
page's existing themes. Keep summaries short, avoid repeating existing entries,
and include the official source link for every new item. Do not invent dates,
features, or claims. Edit only `site/content/github-info.md`, preserving its
editorial focus and structure.

If either source cannot be fetched or the required repository files are
unavailable, use `report_incomplete` and explain what was inaccessible. If the
sources contain no useful, verifiable update or the page needs no meaningful
change, use `noop` with a brief reason. When you make a meaningful change,
Open a pull request for Mona to review; never write
directly to `main`.
