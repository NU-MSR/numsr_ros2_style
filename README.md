# numsr_ros2_style

Replacement for the standard ROS 2 ament_lint tests to make them more compatible with
[ruff](https://docs.astral.sh/ruff/) configurations and google-style doc strings.

1. Copy `ruff.toml` into your repository's root directory, and the files in `test/` into each
   package's `test/` directory (overwriting the stock ROS 2 files). When the package is the
   repository root, these are the same place.
2. From your package directory `ruff format . && ruff check --fix`
3. `ruff` will flag some items that need to be manually fixed.
4. Your package should pass most `colcon test` checks from `ament_flake8` and `ament_pep257`.

# Differences from the ROS 2 defaults
- **flake8** ignores `E203` (whitespace before `:` in `x[a + 1 :]` slices) and `CNL100`
  (blank line after `class Foo:`).
- **pep257** ignores `D406`/`D407` (numpy section header colon and dashed underline), so
  docstrings may be numpy, Google, or reST.

## Known gaps

`ruff` ignores unused imports in a package's `__init__.py`, so `ament_flake8` reports them
(`F401`) instead. Fix them by listing the names in `__all__`, not with `import x as x`,
which `ament_flake8` rejects. ruff has no option to make its own fix use `__all__`
([astral-sh/ruff#15858](https://github.com/astral-sh/ruff/issues/15858)).
