## Deviations

The implementation followed the planned approach of updating `_should_skip_file()` to normalize path separators and exclude generated directories using directory components.

One adjustment was necessary: I removed the `@pytest.mark.xfail` decorators from `test_node_modules_excluded` and `test_build_directory_excluded`. My original plan mentioned these markers but did not explicitly include removing them. The repository's contribution guidance requires removing the markers once the issue is fixed so the tests pass normally in CI.

During implementation, I also corrected a Python indentation error before running the tests.

**Verification results:**
- Before the fix: 2 regression tests failed.
- After the fix: both regression tests passed.
- Full technology detector test file: 27 passed, 0 failed.
- Implementation committed and pushed to my fork on branch `fix/57-exclude-generated-files`.

No changes were made to the language mappings or primary-language selection logic.
