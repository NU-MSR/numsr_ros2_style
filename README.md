# numsr_ros2_style

Replacement for the standard ROS 2 ament_lint tests to make them more compatible with
[ruff](https://docs.astral.sh/ruff/) configurations and google-style doc strings.

1. Copy the files in this directory into your repository (overwriting the stock ROS 2 files)
2. From your package directory `ruff format . && ruff check --fix`
3. `ruff` will flag some items that need to be manually fixed.
3. Your package should pass most `colcon test` checks from `ament_flake8` and `ament_pep257`.

# Differences from the ROS 2 defaults
- **flake8** ignores `E203` (whitespace before `:` in `x[a + 1 :]` slices) and `CNL100`
  (blank line after `class Foo:`). 
- **pep257** ignores `D406`/`D407` (numpy section header colon and dashed underline), so
  docstrings may be numpy, Google, or reST.

## Known gaps

`colcon test` can still fail after a clean ruff run on an unused relative import in a
package's `__init__.py` (list it in `__all__` instead).
