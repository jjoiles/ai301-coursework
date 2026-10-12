# Implementation Plan — Issue #57

**Issue:** https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57

**Contributor:** jjoiles

**Implementation branch:** `fix/57-exclude-generated-files`

## Problem and Reproduction Evidence

The technology detector includes generated and vendored files when determining repository languages. This can incorrectly identify JavaScript as the primary language of a Python project.

I reproduced the issue using the existing regression tests in `tests/unit/test_tech_detector.py`.

Command:

`python -m pytest tests/unit/test_tech_detector.py -k "test_node_modules_excluded or test_build_directory_excluded" -v --runxfail`

Before implementation, both tests failed:

- `test_node_modules_excluded`: expected Python, received JavaScript.
- `test_build_directory_excluded`: expected Python, received JavaScript.

The reproduction evidence is documented in my issue comment:

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57#issuecomment-6000149101

## Diagnosis

The `_should_skip_file()` method in `agent/tools/tech_detector.py` checks directory patterns such as `/node_modules/` and `/build/`.

However, repository-relative paths such as `node_modules/package1/index.js` and `build/generated.js` do not contain the leading slash required by these patterns.

As a result, the generated files pass through the filter and contribute to language detection.

## Proposed Implementation

1. Update `_should_skip_file()` in `agent/tools/tech_detector.py` to normalize Windows and Unix path separators.
2. Identify excluded directory names using path components rather than requiring a leading slash.
3. Preserve the existing excluded-directory list, including `node_modules`, `vendor`, `dist`, `build`, `.git`, `__pycache__`, `.venv`, and `venv`.
4. Ensure that legitimate source files remain eligible for language detection.
5. Keep the change limited to generated-directory filtering. Do not modify language mappings, primary-language selection, or unrelated detection behavior.

## Verification Plan

Rerun the two existing regression tests:

`python -m pytest tests/unit/test_tech_detector.py -k "test_node_modules_excluded or test_build_directory_excluded" -v --runxfail`

Expected result: both tests pass and identify Python as the primary language.

Also verify root-level and nested generated directories, Windows-style paths, and legitimate paths with similar but nonexcluded directory names.

Run the complete technology detector test file:

`python -m pytest tests/unit/test_tech_detector.py -v --runxfail`

Expected result: no regressions in the existing detector tests.

Compare the before-and-after test output and record the results in the Unit 7 writeup.

## Risks and Limitations

The fix must not exclude legitimate directories whose names merely contain an excluded name, such as `my_build` or `node_modules_backup`.

Path normalization should not change the behavior of unrelated language or framework detection.

The existing regression tests are marked `xfail(strict=True)`, so verification will use `--runxfail` to execute their assertions normally.

## Deviations

To be completed after implementation. I will document whether the completed change followed this plan and explain any differences before submitting the assignment.
