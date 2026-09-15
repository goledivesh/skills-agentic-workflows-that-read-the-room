---
name: update-github-info
model: gpt-5
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
tools:
  github:
    toolsets:
      - repos
  edit: {}
  web-fetch: {}
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    max: 1
    draft: true
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Keep Mona's GitHub Info website current with concise, practical updates backed by official GitHub sources.

1. Use GitHub repository API tools to read `notes/mona-notes.md` and any repository guidance or reference files needed for this task. Do not use terminal, CLI, or sandboxed commands to read repository guidance or reference files.
2. Use `web-fetch` to read https://github.blog/latest/.
3. Use `web-fetch` to read https://github.blog/changelog/.
4. Use `web-fetch` to read https://awesome-copilot.github.com/workflows/.
5. Review the current `site/content/github-info.md` through the repository API tools before editing it.
6. Update only `site/content/github-info.md` with short, practical, source-backed information that helps developers learn GitHub faster. Mention the source whenever a change comes from the GitHub Blog, GitHub Changelog, or Awesome Copilot workflows, and preserve the existing editorial direction.
7. Use the `create-pull-request` safe output to propose the change for Mona to review. Do not write directly to the default branch. If no meaningful update is supported by the fetched sources, do not create a pull request.
