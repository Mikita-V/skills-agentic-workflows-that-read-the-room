---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read
  pull-requests: read

tools:
  github:
    toolsets: [repos]
  web-fetch:
  edit:

network:
  allowed:
    - github.blog
    - github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: true
---

# Update GitHub Info

Keep the GitHub Info website current with concise, practical updates for developers.

## Research

1. Read `notes/mona-notes.md` using the GitHub repository API tools. Use those tools for repository guidance and reference files; do not use terminal, CLI, or sandboxed commands for those reads.
2. Read the current `site/content/github-info.md` using the GitHub repository API tools.
3. Use the `web-fetch` tool to fetch https://github.blog/latest/.
4. Use the `web-fetch` tool to fetch https://github.blog/changelog/.

## Update

Identify only useful, recent GitHub Blog or GitHub Changelog items that fit Mona's editorial angle. Keep summaries short and practical, explain why each item matters to developers, and include the official source link for every new item. Preserve the existing Markdown structure and avoid duplicating items already present.

Use the `edit` tool to update `site/content/github-info.md` only when there is a worthwhile change. Do not modify unrelated files, workflow files, or generated files. Do not write directly to `main`.

## Review

When an update is needed, use the `create-pull-request` safe output to open a draft pull request containing the change for Mona to review. Describe the sources consulted and summarize the proposed content in the pull request body. If no worthwhile update is found, do not create a pull request.