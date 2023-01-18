# type-ignore
Add `# type: ignore [error_code]` and remove unused `#type: ignore`s

When you refactor code to use type annotations you cannot fix every violations at once you can add `# type: ignore [error-code]` comments to let `mypy` pass.
When you further refine your annotations some of these lines may become valid and the `# type: ignore` comments have to be removed.
With `type-ignore` it is possible to automate this process.

# Usage

Either pipe the output of `mypy` directly into type-ignore

```
mypy type_ignore | type-ignore remove --dry-run
```

or you can use a file to read the error information from
```
mypy type_ignore > errors.txt
type_ignore add --error-file=mypy_error_report.txt --dry-run
```

The `--dry-run` flag lets you see what would be changed without modifying your code.
Files are modified in place, **it is strongly recommended to `git commit` before running this tool**.

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

# Alternatives

At the time I wrote this I could not find a tool to add and remove type ignore comments, only after I published this on GitHub :octocat: I found out that I reinvented the wheel 🤦️.

- [mypy-silent](https://github.com/whtsky/mypy-silent) - Automatically add or remove `# type: ignore` comments to silence mypy. Inspired by `pylint-silent`.
- [mypy_clean_slate](https://github.com/geo7/mypy_clean_slate) - CLI tool for providing a clean slate for mypy usage within a project.

Another tool that tries solve the same problem, but with a different approach and many more features is:
- [mypy-baseline](https://github.com/orsinium-labs/mypy-baseline) - A CLI tool for painless integration of mypy with an existing Python project. When you run it for the first time, it will remember all type errors that you already have in the project (generate "baseline"). All consecutive runs will ignore these errors and report only ones that you introduced after that.

Check out the [Awesome Python Typing](https://github.com/typeddjango/awesome-python-typing#working-with-types) [![Awesome](https://awesome.re/badge-flat2.svg)](https://awesome.re) list.
