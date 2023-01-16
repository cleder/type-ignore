# type-ignore
Add `# type: ignore [error_code]` and remove unused `#type: ignore`s

When you refactor code to use type annotations you may have to add some
`# type: ignore [error-code]` comments to let `mypy` pass.
When you further refine your annotations some of these lines may become valid
and the `# type: ignore` comments have to be removed.
With `type-ignore` it is possible to automate this process.

# Usage

Either pipe the output of `mypy` directly into type-ignore

```
mypy type_ignore | type-ignore remove --dry-run
```

or you can use a file to read the error information from
```
mypy type_ignore > errors.txt
type_ignore add --error-file errors.txt --dry-run
```

Always `git commit` before running this tool.

# Mypy configuration

Add this to your `mypy` configuration:
```
[tool.mypy]
...
warn_unused_ignores = true
show_error_codes = true
enable_error_code = [
    "ignore-without-code"
]
```
