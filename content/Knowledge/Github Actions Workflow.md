Parent:: [[github actions ontology]]

# Summary
A configuration for an automated process can contain one or more job. Can be triggered via event, manually, or scheduled.

They are configured with a file in your repository `.github/workflows`. You can reference a workflow in another workflow - [[Reusing Workflows]]

# Body

[[Workflow File]]

Same of a workflow from docs
```yaml
name: learn-github-actions
run-name: ${{ github.actor }} is learning GitHub Actions
on: [push]
jobs:
  check-bats-version:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v3
        with:
          node-version: '14'
      - run: npm install -g bats
      - run: bats -v

```