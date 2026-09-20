---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read

network:
  allowed:
    - github.blog
    - github.com

tools:
  web-fetch:
  edit:
  github:
    toolsets: [repos]

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: false
    if-no-changes: warn
---

# Update GitHub Info

Update the website content with the latest official GitHub news and changelog entries.

## Required process

1. Read `notes/mona-notes.md` to understand Mona's notes and context.
2. Use `web-fetch` to read these public pages:
   - https://github.blog/latest/
   - https://github.blog/changelog/
3. Use GitHub repository API tools (through the `github` tool) to read any repository guidance or reference files you need.
4. Do not use terminal commands, CLI commands, or sandboxed bash commands for repository guidance collection.
5. Update `site/content/github-info.md` with a concise, accurate summary of relevant updates.
6. Propose the change with the `create-pull-request` safe output so Mona can review before merge.

## Output expectations

- Keep the page factual and concise.
- Include links to source items where useful.
- Do not push directly to the default branch.