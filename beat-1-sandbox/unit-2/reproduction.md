# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

jjoiles

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57#issuecomment-5999392681

Hi, I'd like to investigate the issue with `tech_detector.py` including paths under `node_modules/` and `build/` when those generated directories should be excluded. I'll reproduce the reported behavior first, review the relevant exclusion logic, and report back with what I find.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/57#issuecomment-6000149101

I was able to reproduce the reported behavior for issue #57.

Environment:
- Windows 11
- Python 3.14.7
- pytest 9.1.1
- Repository: codepath/pathreview-ai301-fa26-howard

Steps:
1. Cloned the repository.
2. Installed the project and development dependencies with:
   `python -m pip install -e ".[dev]"`
3. 3. Ran a direct reproduction with:
   `python -c "from agent.tools.tech_detector import TechDetector; t=TechDetector(); files=['main.py','core/app.py','node_modules/lib/util.js','node_modules/x/a.js','node_modules/y/b.js','build/bundle.js','build/vendor.js']; print(t.execute({'files': files}).data['primary_language'])"`
4. Ran the two tests associated with issue #57 with:
   `python -m pytest tests/unit/test_tech_detector.py -k "test_node_modules_excluded or test_build_directory_excluded" -v --runxfail`

Observed result:
The direct reproduction returned:

`primary_lang=JavaScript`

`JavaScript`

The two issue-specific tests also failed:

- `TestTechDetector::test_node_modules_excluded` — `AssertionError: assert 'JavaScript' == 'Python'`
- `TestTechDetector::test_build_directory_excluded` — `AssertionError: assert 'JavaScript' == 'Python'`

Pytest reported:

`2 failed, 25 deselected in 0.35s`

This reproduces the behavior described in issue #57: JavaScript files under `node_modules/` and `build/` are being counted, causing the detector to report JavaScript as the primary language when Python should be reported. I have not changed the implementation.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

12/17 scored, with 3 packages erroring because of a Windows UTF-8 encoding issue.
18/20 PASS.
19/20 PASS.

**Package analysis**

pkg-05 — My rubric decided reject, while the gold label said accept. The package described creating a minimal `env.yml` with dependencies and a category, but it did not provide the literal contents needed to recreate that input. My Reproduction steps check therefore treated an essential reproduction input as missing, even though the gold label considered the described setup sufficient for a reader familiar with the tool.

**Check rationale**

"Pass if the stated steps provide enough concrete setup information, commands, inputs, and actions for another person familiar with the relevant tool to recreate the reproduction attempt and reach the reported outcome. Minor details that are reasonably inferable from the described setup do not cause failure; fail only when an essential step or input needed to perform the reproduction is missing."

I revised this Reproduction steps check because an earlier version was too strict about details that an experienced user could reasonably infer. The final wording keeps essential commands and inputs required while allowing minor inferable details, which better distinguishes an actually unfollowable reproduction from one that is sufficiently reproducible.

**Trade-offs**

The final Reproduction steps wording improved agreement by allowing minor details that are reasonably inferable, but it still rejected pkg-05 because the missing input was interpreted as essential rather than minor. I accepted that trade-off instead of loosening the check further, because doing so could allow reproduction packages to pass even when a stranger does not have enough information to recreate the reported outcome. I re-ran pkg-05 as part of the targeted and canary testing while tuning this check, and the final full evaluation reached 19/20 agreement.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
