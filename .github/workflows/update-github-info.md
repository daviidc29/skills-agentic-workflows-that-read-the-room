---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
engine: copilot
model: gpt-4.1
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
tools:
  edit:
  web-fetch:
  github:
    toolsets: [repos]
safe-outputs:
  create-pull-request:
    draft: true
    title-prefix: "[mona] "
---

# Update GitHub Info

Keep the GitHub Info website current for Mona's review.

1. Read `notes/mona-notes.md` before making any changes.
2. Use the web-fetch tool to read https://github.blog/latest/.
3. Use the web-fetch tool to read https://github.blog/changelog/.
4. Use the web-fetch tool to read https://awesome-copilot.github.com/workflows/.
5. Use the GitHub repository API tools, not terminal, CLI, or sandboxed commands, to read repository guidance or reference files.
6. Use the edit tool to update `site/content/github-info.md` with short, practical developer-focused summaries. Mention the source whenever an update comes from the GitHub Blog, GitHub Changelog, or Awesome Copilot workflows.
7. Review the resulting diff and make only focused content updates. Do not modify generated workflow files or unrelated files.
8. If `site/content/github-info.md` changed, request the `create_pull_request` safe output exactly once with a concise title and body explaining the sources reviewed and the changes made. The pull request must propose the changes for Mona to review and must not write directly to `main`.
9. If there are no useful changes, do not create a pull request and report that no update was needed.