#  Issues Generation

This solution is broken into two parts:

1. A CLI set of entry points that provides utility functions
2. A default entrypoint for GitHub actions to manage "queued" issues.

### Terminology

- **Queued Issue:** An issue that is to be created when the PR is merged.

## Usage

### CLI

#### Install

```shell
npm i -g issues-generation
```

#### Usage

```shell
$ issues-generation --help
Usage: issues-generation [options] [command]

Options:
  -h, --help        display help for command

Commands:
  action            process GitHub Action events
  list [options]    list queued issues for a pull request
  create [options]  create queued issues for a pull request
  help [command]    display help for command
```

### GitHub Actions

#### Usage

```yaml
name: Issues Generation

concurrency: issues-generation

on:
  issue_comment:
    types: [created]
  pull_request_review_comment:
    types: [created]
  pull_request_target:
    types: [opened, reopened]

jobs:
  issue-generation-bot:
    if: ${{ github.event.issue.pull_request || github.event.pull_request }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Run Issue Generation
        uses: jromero/issue-generation-action@v1.0.0-beta.4
        id: issues-generation
        with:
          github-token: ${{ secrets.BOT_GITHUB_TOKEN }}
          bot-username: my-bot-account

```

## Development

When done making all your changes, run the following command to lint, test and compile:

```shell
npm run prepare-for-pr
```
