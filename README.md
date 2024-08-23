# Action: Setup tree-sitter parser

This is an action to install tree-sitter cli and build tree-sitter parser.

## Inputs

### `parser_dir`

Directory to store built parser shared library.
The default is `./parser`.

### `parser_repository`

**Required**

Parser repository name to build.

## Usage

When using [reviewdog/action-ast-grep][reviewdog/action-ast-grep] for custom language, it is useful to build parser by using this action.

```yaml
name: reviewdog
on: [pull_request]
jobs:
  ast-grep:
    name: runner / ast-grep / fennel
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Build tree-sitter grammar for fennel
        uses: rinx/setup-tree-sitter-parser@v1
        with:
          # this action will place the build artifact here.
          parser_dir: ./
          parser_repository: alexmozaidze/tree-sitter-fennel
      - name: Run ast-grep with reviewdog
        uses: reviewdog/action-ast-grep@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          level: info
          reporter: github-pr-review
```

[reviewdog/action-ast-grep]: https://github.com/reviewdog/action-ast-grep
