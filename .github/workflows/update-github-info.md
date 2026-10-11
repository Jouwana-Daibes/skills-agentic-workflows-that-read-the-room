---
name: update-github-info
description: Review recent GitHub Blog and Changelog updates and propose practical updates to GitHub Info for Mona.
engine:
  id: copilot
  model: gpt-5
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    draft: false
    max: 1
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and the current `site/content/github-info.md`. Fetch these sources:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Use web fetch to retrieve https://awesome-copilot.github.com/workflows/.

Select recent, relevant developments that help developers learn GitHub faster. Verify details against the fetched sources, keep summaries short and practical, and include a link to the originating source for every update. Edit only `site/content/github-info.md`, preserving its existing editorial direction and concise format.

If neither source contains a relevant, verifiable update, leave the file unchanged and call `noop` with a brief reason. Otherwise, use the `create-pull-request` safe output to open one non-draft pull request for Mona to review. Make the title and body clearly explain the updates and link to their sources. Do not write directly to the default branch or use another mechanism to create a pull request.
