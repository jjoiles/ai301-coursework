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

The implementation followed the planned approach of updating `_should_skip_file()` to normalize path separators and exclude generated directories using directory components.

One adjustment was necessary: I removed the `@pytest.mark.xfail` decorators from `test_node_modules_excluded` and `test_build_directory_excluded`. My original plan mentioned these markers but did not explicitly include removing them. The repository's contribution guidance requires removing the markers once the issue is fixed so the tests pass normally in CI.

During implementation, I also corrected a Python indentation error before running the tests.

Plan-file note: an earlier revision of this file (commit `7aae046`) accidentally replaced the plan body with only this Deviations section. The original plan above is restored unchanged from commit `275ba5e`; only this section is new.

**Verification results:**
- Before the fix: 2 regression tests failed (`AssertionError: assert 'JavaScript' == 'Python'`).
- After the fix: both regression tests passed.
- Full technology detector test file: 27 passed, 0 failed.
- Edge-case checks against the committed `_should_skip_file()`:

  | Path | Skipped? | Expected |
  |---|---|---|
  | `node_modules/a.js` (root-level) | yes | yes |
  | `src/node_modules/a.js` (nested) | yes | yes |
  | `a/build/b.js` (nested) | yes | yes |
  | `build\x.js` (Windows-style separator) | yes | yes |
  | `my_build/x.js` (similar name) | no | no |
  | `node_modules_backup/a.js` (similar name) | no | no |
  | `build.py` (file, not directory) | no | no |

- Implementation committed and pushed to my fork on branch `fix/57-exclude-generated-files` (commit `6a6c58f`).

No changes were made to the language mappings or primary-language selection logic, and the restored Risks section's false-positive concern is covered by the similar-name rows above.
