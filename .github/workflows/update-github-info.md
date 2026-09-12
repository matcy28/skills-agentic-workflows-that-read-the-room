---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:
  stop-after: "+48h"
permissions:
  contents: read
  pull-requests: read
network:
  allowed:
    - github.blog
    - github.com
tools:
  github:
    toolsets:
      - repos
  web-fetch: {}
  edit: {}
safe-outputs:
  create-pull-request:
    max: 1
    draft: true
    reviewers:
      - mona
---

# Update GitHub Info

Update the GitHub Info website content so Mona can review a small, sourced change.

## Required process

1. Read `notes/mona-notes.md` first with the GitHub repository API tools. Follow its writing and review requirements.
2. Read the repository guidance or reference files needed for this task with the GitHub repository API tools. Do not use terminal, CLI, or sandboxed commands for repository reads.
3. Read external public guidance about GitHub Agentic Workflows with `web-fetch` from the public GitHub repository at `https://github.com/github/gh-aw/blob/main/README.md`. Use this guidance only to inform workflow-safe behavior.
4. Fetch `https://github.blog/latest/` with `web-fetch` and identify a concise, practical developer update relevant to the site.
5. Fetch `https://github.blog/changelog/` with `web-fetch` and identify a concise, practical developer update relevant to the site.
6. Update only `site/content/github-info.md` with short, practical summaries. Mention the source for every item derived from the GitHub Blog or GitHub Changelog.
7. Review the diff using the available file and repository tools. Do not modify workflow files, generated files, or unrelated content.
8. If there is no useful, well-sourced update, do not invent one and do not request a pull request.
9. When `site/content/github-info.md` has a worthwhile change, use the `create-pull-request` safe output to open a draft pull request for Mona to review. Never write directly to `main`.

The workflow is temporary: after 48 hours from compilation, stop processing scheduled and manual runs.