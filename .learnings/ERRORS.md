# Errors

Command failures and integration errors.

---

## [ERR-20260811-003] powershell_regex_index_validation

**Logged**: 2026-08-11T00:00:00+08:00
**Priority**: low
**Status**: resolved
**Area**: tests

### Summary
A PowerShell-embedded Node command failed while extracting `PAGE_INDEX` because shell escaping changed the regular expression.

### Context
- The browser QA already verified that the navigation rendered five records and filtered the new page correctly.
- The failure was limited to the ad hoc completeness command, not the HTML or navigation runtime.

### Suggested Fix
Prefer direct file/path checks or a temporary native script when validating JavaScript data embedded in HTML; avoid multi-layer regex escaping in PowerShell.

### Metadata
- Reproducible: yes
- Related Files: _qa_dms.cjs, index.html

### Resolution
- **Resolved**: 2026-08-11T00:00:00+08:00
- **Notes**: The browser check was rerun successfully with the bundled Playwright runtime; the temporary validation scripts are removed before delivery.

---

## [ERR-20260811-003] anysearch_connection_error

**Logged**: 2026-08-11T00:00:00+08:00
**Priority**: medium
**Status**: fallback-used
**Area**: research

### Summary
AnySearch Node CLI returned `Connection Error` while searching for AI curriculum and automotive AI sources.

### Context
Node.js 24.17.0 was available and the configured CLI script loaded successfully; the failure occurred during the remote request.

### Suggested Fix
Use the current web research tool for authoritative sources when AnySearch has a transient endpoint or network failure, and retry AnySearch in a later run.

### Resolution
Fallback to official course, standards, and regulator pages discovered through web search; no secrets or response payloads were logged.

---

## [ERR-20260811-003] powershell_nested_variable_expansion

**Logged**: 2026-08-11T00:00:00+08:00
**Priority**: low
**Status**: resolved
**Area**: config

### Summary
A nested PowerShell version probe failed because `$PSVersionTable` was expanded by the outer PowerShell command before the inner command ran.

### Context
- Command attempted during AnySearch Skill runtime detection.
- The failing shape was `powershell -Command "$PSVersionTable.PSVersion.ToString()"` from an already-running PowerShell shell.

### Suggested Fix
Avoid nested PowerShell for simple probes, or quote with single quotes / escape `$` so the variable is evaluated by the intended shell.

### Metadata
- Reproducible: yes
- Related Files: C:\Users\10902\.codex\skills\anysearch\SKILL.md

### Resolution
- **Resolved**: 2026-08-11T00:00:00+08:00
- **Notes**: Used the available Node.js runtime for AnySearch verification instead.

---

## [ERR-20260805-005] skills_cli_git_clone_connection_reset

**Logged**: 2026-08-05T00:00:00+08:00
**Priority**: low
**Status**: resolved
**Area**: infra

### Summary
The recommended `npx skills add` command failed while cloning a large GitHub repository because the connection was reset.

### Error
```
fatal: unable to access the GitHub repository: Recv failure: Connection was reset
```

### Context
- The CLI attempted a full clone of `affaan-m/ECC` even though only one nested skill directory was required.
- The destination skill directory had not been created, so no partial installation remained.

### Suggested Fix
Use the system skill installer's direct GitHub download helper with the exact nested skill path.

### Metadata
- Reproducible: unknown
- Related Files: none

### Resolution
- **Resolved**: 2026-08-05T00:00:00+08:00
- **Notes**: Direct-download installation of `docs/zh-CN/skills/prompt-optimizer` completed successfully.

---

## [ERR-20260805-004] powershell_npx_ps1_execution_policy

**Logged**: 2026-08-05T00:00:00+08:00
**Priority**: low
**Status**: resolved
**Area**: config

### Summary
PowerShell resolved `npx` to `npx.ps1`, which was blocked by the system execution policy.

### Error
```
PSSecurityException: npx.ps1 cannot be loaded because running scripts is disabled.
```

### Context
- Attempted to query the local npx version before installing a skill.
- The Node installation also provides `npx.cmd`, which does not require changing PowerShell policy.

### Suggested Fix
On Windows PowerShell environments with restricted script execution, invoke `npx.cmd` explicitly.

### Metadata
- Reproducible: yes
- Related Files: none

### Resolution
- **Resolved**: 2026-08-05T00:00:00+08:00
- **Notes**: Use `npx.cmd` for the installation command.

---

## [ERR-20260805-001] playwright_module_unavailable

**Logged**: 2026-08-05T00:00:00+08:00
**Priority**: low
**Status**: resolved
**Area**: tests

### Summary
Bundled workspace Python did not include the Playwright module during static HTML visual QA.

### Error
```
ModuleNotFoundError: No module named 'playwright'
```

### Context
- Attempted native Python Playwright rendering of a local single-file HTML page.
- The workspace dependency helper exposed Python and Node runtimes, but not Playwright.

### Suggested Fix
Use the bundled Node Playwright package with the installed Microsoft Edge executable, or verify the Python Playwright module before creating the test script.

### Metadata
- Reproducible: yes
- Related Files: _check_kg_page.py
- Pattern-Key: tests.python_playwright_unavailable
- Recurrence-Count: 2
- First-Seen: 2026-08-05
- Last-Seen: 2026-08-05

### Resolution
- **Resolved**: 2026-08-05T00:00:00+08:00
- **Notes**: Switched to Node Playwright and launched the installed Edge binary via `executablePath`.

---

## [ERR-20260805-002] direct_edge_headless_sandbox_failure

**Logged**: 2026-08-05T00:00:00+08:00
**Priority**: low
**Status**: resolved
**Area**: tests

### Summary
Direct PowerShell invocation of Edge headless failed to produce screenshots in the managed sandbox.

### Error
```
GPU process isn't usable; screenshot file was not created.
```

### Context
- Edge was started directly with a dedicated user-data directory and `--disable-gpu`.
- Registry and GPU cache access failed in the managed Windows environment.

### Suggested Fix
Drive the installed Edge binary through Node Playwright, which correctly manages the browser process and captures diagnostics.

### Metadata
- Reproducible: yes
- Related Files: 02-concepts/knowledge-graph-ontology/知识图谱×本体论-概念精读-20260805.html

### Resolution
- **Resolved**: 2026-08-05T00:00:00+08:00
- **Notes**: Node Playwright completed desktop/mobile rendering, interaction checks, and screenshots with zero console errors.

---

## [ERR-20260805-003] node_repl_dynamic_code_restriction

**Logged**: 2026-08-05T00:00:00+08:00
**Priority**: low
**Status**: resolved
**Area**: tests

### Summary
The Node REPL security policy rejected `new Function()` during inline JavaScript syntax validation.

### Error
```
Code generation from strings disallowed for this context
```

### Context
- Attempted to compile the HTML's embedded script without executing it.
- Browser execution had already completed without page errors.

### Suggested Fix
Extract the script to an exact temporary file and run the bundled Node executable with `--check`, then remove the temporary file.

### Metadata
- Reproducible: yes
- Related Files: 02-concepts/knowledge-graph-ontology/知识图谱×本体论-概念精读-20260805.html

### Resolution
- **Resolved**: 2026-08-05T00:00:00+08:00
- **Notes**: Bundled Node `--check` returned successfully and the temporary file was removed.

---

## [ERR-20260805-006] system_python_missing_pyyaml

**Logged**: 2026-08-05T00:00:00+08:00
**Priority**: low
**Status**: resolved
**Area**: tests

### Summary
Neither the shell-default Python nor the bundled Codex Python could run the skill-creator validation script because PyYAML was unavailable.

### Error
```
ModuleNotFoundError: No module named 'yaml'
```

### Context
- Attempted to run `skill-creator/scripts/quick_validate.py --help` with the shell-default Python.
- Retried with the Codex workspace Python runtime; it has no `yaml` module either.

### Suggested Fix
Use a Python runtime that already provides PyYAML, or perform a small manual frontmatter and JSON validation without adding a project dependency.

### Metadata
- Reproducible: yes
- Related Files: .agents/skills/ai-research-html/SKILL.md

### Resolution
- **Resolved**: 2026-08-05T00:00:00+08:00
- **Notes**: Manual frontmatter/JSON checks were used; no dependency was installed into the repository.

---

## [ERR-20260811-001] qa_filter_state_not_reset

**Logged**: 2026-08-11T00:00:00+08:00
**Priority**: low
**Status**: resolved
**Area**: tests

### Summary
The first browser QA pass reported a false navigation-filter failure because the test kept a text search active while changing the direction filter.

### Context
- The product page rendered correctly with no console errors or horizontal overflow.
- The test sequence searched for `PPAP`, then clicked the automotive direction filter without clearing the search term.

### Suggested Fix
Reset or explicitly compose filter state between independent interaction assertions.

### Metadata
- Reproducible: yes
- Related Files: _qa_process.cjs, index.html

### Resolution
- **Resolved**: 2026-08-11T00:00:00+08:00
- **Notes**: The QA script now clears the search before testing the independent direction filter.

---

## [ERR-20260811-002] powershell_regex_newline_false_positive

**Logged**: 2026-08-11T00:00:00+08:00
**Priority**: low
**Status**: resolved
**Area**: tests

### Summary
A one-line Node validation command reported a missing Skill frontmatter because PowerShell altered the regular-expression newline escaping.

### Context
- The Skill file has valid frontmatter and was already discoverable by the Codex skill catalog.
- The failure occurred only in the shell-embedded assertion.

### Suggested Fix
Use direct string-prefix checks for simple frontmatter assertions when invoking Node through PowerShell.

### Metadata
- Reproducible: yes
- Related Files: .agents/skills/ai-research-html/SKILL.md

### Resolution
- **Resolved**: 2026-08-11T00:00:00+08:00
- **Notes**: Replaced the regex assertion with a direct prefix check.

---
