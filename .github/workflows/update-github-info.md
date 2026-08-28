---
name: update-github-info
description: Keep the GitHub Info page current with practical updates from official GitHub sources.

on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read

tools:
  github:
    mode: local
    toolsets: [repos]
  edit: true
  web-fetch:

network:
  allowed:
    - defaults
    - github.blog
    - github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: true
    allowed-files:
      - "site/content/github-info.md"
---

Keep the GitHub Info website current for Mona.

1. Read `notes/mona-notes.md` first. Treat it as repository guidance.
2. Use the GitHub repository API tools to read repository guidance and reference files, including `notes/mona-notes.md` and `site/content/github-info.md`. Do not use terminal, CLI, or sandboxed commands for those reads.
3. Use `web-fetch` to read both official sources:
   - https://github.blog/latest/
   - https://github.blog/changelog/
4. Select only useful, recent updates that fit Mona's practical developer-focused editorial angle. Keep summaries short and practical, and mention the source for every blog or changelog item.
5. Update `site/content/github-info.md` with the selected information while preserving its existing structure and editorial themes. Do not modify any other file.
6. When the content needs updating, use the `create-pull-request` safe output to open a draft pull request for Mona to review. Describe the sources and the changes in the pull request body. Never write directly to `main`.
7. If no worthwhile update is available, make no file changes and use `noop` instead of opening an empty pull request.
