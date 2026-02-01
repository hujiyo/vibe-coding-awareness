# README

## EN

# Vibe Coding Awareness

### Overview

**vibe-coding-awareness** is a skill brief for AI agents or developers inheriting multi-agent / AI-generated codebases. It packs the mindset, decision rules, and cleanup rituals required to turn residue-heavy repositories into maintainable systems.

### Repository Layout

```
.
├── LICENSE            # Apache-2.0 license
└── skill/
    └── SKILL.md       # Full skill specification
```

### How to Use

1. **Read the skill**: Start with `skill/SKILL.md` to internalize the core assumption—assume residue, prefer cleanup.
2. **Apply the checklists**: Use the provided detection patterns (duplicate logic, versioned files, commented fossils) during audits.
3. **Report succinctly**: Follow the Removal/Consolidation summary templates when communicating changes to other agents.
4. **Iterate intentionally**: Lean on the language-specific guidance (Section 10) to standardize the stack as you modify files.

### When to Reach for This Skill

- The user mentions “vibe coding”, “AI-generated”, or “multiple agents worked on this project”.
- You encounter overlapping utilities, partial refactors, or abandoned components.
- Documentation/context from human authors is missing, yet decisive cleanup is required.

### Contributing

Issues and PRs are welcome for new cleanup recipes, tooling, or clarifications. Please ensure additions reinforce the “clean first, consolidate fast” philosophy.

### License

Distributed under the [Apache License 2.0](./LICENSE).

---

## CN

# Vibe Coding Awareness

### 项目简介

**vibe-coding-awareness** 一份面向接手“多代理/AI 残留”代码库的 AI 代理或工程师的技能说明书。它总结了识别残留、果断删除与统一实现的实战规则，让你迅速把混乱仓库恢复为可维护状态。

### 目录结构

```
.
├── LICENSE            # 项目许可证（Apache-2.0）
└── skill/
    └── SKILL.md       # 技能全文
```

### 如何使用

1. **阅读技能文档**：打开 `skill/SKILL.md`，先建立“默认残留、优先清理”的心智模型。
2. **执行检查清单**：对照文档中的检测模式（重复实现、版本后缀、注释化骨架等）逐项排查。
3. **记录结论**：使用 Removal/Consolidation Summary 模板，快速汇报本次处理范围与结果。
4. **持续迭代**：结合第 10 章“语言特定模式”，在修改文件时同步统一代码风格与依赖。

### 适用场景

- 用户提及 “vibe coding” / “AI 生成” / “多代理协作”。
- 代码库出现大量重复逻辑、半完成重构、未引用文件或版本后缀命名。
- 在缺乏人类上下文的前提下，需要迅速做出清理与整合决策。

### 贡献方式

欢迎通过 Issue 或 Pull Request 提出案例、脚本或流程优化建议，前提是保持“清理优先、统一实现”的核心原则。

### 许可证

本项目遵循 [Apache License 2.0](./LICENSE)，使用或分发前请先阅读相关条款。
<details>
<summary><strong>content</strong></summary>
---
name: vibe-coding-awareness
description: |
  Awareness and decision rules for editing vibe-coded projects - codebases primarily produced by multiple AI agents over time. This skill assumes unused or duplicated code is more likely residual AI output than intentional human design. Use when: user mentions "vibe coding" / "AI-generated" / "multiple agents worked on this", or when detecting duplicated logic, orphaned functions, partial refactors, inconsistent patterns, or version-suffixed code (handleXNew, ComponentV2).
---

# Vibe Coding Awareness

## 0. Core Assumption (Non-Negotiable)

This project is **AI-dominated** in authorship, having been iteratively modified by multiple AI agents without centralized architectural oversight.

**Default Attribution Rule:**
When encountering unused, duplicated, or inconsistent code, assume:
- It is **residual output from previous AI iterations**
- Human intentional preservation is the **exception**, not the default
- Version control, not code retention, preserves history

This assumption **overrides** the usual "preserve unless certain" bias that applies to human-authored codebases.

---

## 1. Agent Role & Mindset

You are operating as a **successor agent**, not an original author.

**Implications:**
- You inherit incomplete context and abandoned attempts from prior agents
- You have authority to invalidate previous AI decisions
- Your responsibility is reducing accumulated structural entropy
- You optimize for **current coherence**, not historical faithfulness

**Core Principle:** Each edit is an opportunity to leave the codebase cleaner than you found it.

---

## 2. Decision Framework

### 2.1 Code Removal Priority (Apply in Order)

When evaluating whether to keep code:

1. **Is it referenced or executed anywhere?**
   - If NO → **Strong candidate for removal**
   - Search project-wide: `grep -r "functionName" .`

2. **Is there a newer/clearer implementation elsewhere?**
   - If YES → **Remove older version**, migrate callers if needed
   - Look for version suffixes: `handleSubmitV2`, `getUserDataNew`

3. **Is there explicit human intent documented?**
   - Check for: preserved comments, related tests, design docs
   - If NO → **Do not assume intent**

4. **Would removing this reduce cognitive load?**
   - If YES → **Remove**
   - Fewer lines = easier maintenance

**Conflict Resolution:** When priorities conflict, **favor removal**.

### 2.2 Attribution Rule

**Default Attribution:**
> "This code exists because a previous AI agent created it during an earlier iteration."

**Only override** this attribution when **explicit evidence** exists:
- Comment stating intentional preservation: `// Keep for backward compatibility with v1 API`
- Active test depending on the code
- Documented design decision tied to the code

**Important:** Lack of evidence is **not** evidence of intention.

---

## 3. Common Vibe Coding Artifacts & Actions

### 3.1 Orphaned Functions & Dead Code

**Indicators:**
- Functions defined but never imported/called
- Commented-out code blocks
- Unused imports at file top

**Action:**
```
1. Search for all references: grep -r "functionName" .
2. If only definition found → DELETE
3. If only in tests → Verify test validity, then decide
4. Remove without seeking permission
```

### 3.2 Multiple Implementations of Same Logic

**Indicators:**
```javascript
// Different agents solving same problem independently
handleSubmit()
onSubmit() 
submitForm()
processSubmission()
```

**Action:**
```
1. Identify all similar implementations
2. Choose most complete/recent/robust version
3. Migrate all callers to chosen implementation
4. Delete inferior versions
5. Rename consolidated function if needed for clarity
```

### 3.3 Partial Refactors (Incomplete Migrations)

**Indicators:**
- Old and new patterns coexisting
- Half-migrated code: some components using hooks, others using classes
- Parallel utility files: `utils.js`, `helpers.js`, `utilities.js`

**Action:**
```
Assume the newer pattern reflects current direction:
1. Complete the migration, OR
2. Revert to old pattern for consistency
3. Do NOT preserve both for "safety"

Parallel implementations = technical debt, not flexibility
```

### 3.4 Version Suffix Pattern

**Indicators:**
- `functionNameV2`, `functionNameNew`, `functionNameUpdated`
- `ComponentOld`, `ComponentLegacy`, `Component2`
- Files: `Header.jsx`, `HeaderNew.jsx`, `Header_v2.jsx`

**Action:**
```
1. Suffixed version is likely current
2. Verify by checking recent usage
3. Migrate all references to current version
4. Delete superseded versions
```

### 3.5 Comment Archaeology

**Indicators:**
```javascript
// TODO: Refactor this entire section (from 6 months ago)
// Old implementation below - DO NOT USE
// This used to handle X but now does Y
// FIXME: breaks on edge cases
// Note: Changed approach from X to Y
```

**Action - DELETE these patterns:**
- Historical explanations: `"This used to..."`
- Abandoned TODOs: `"TODO: refactor"` → Do it now or delete
- Warnings about removed code: `"Old implementation: ..."`

**Action - KEEP only:**
- Non-obvious current decisions: `"Edge case: handles X because Y"`
- Performance justifications: `"This approach chosen because Z"`
- Active warnings: `"Warning: don't change X because Y breaks"`

**Rule:** Comments are not authoritative. Treat as potentially stale.

### 3.6 Dependency Confusion

**Indicators:**
- Multiple packages for same purpose: `axios`, `fetch`, `request`
- Unused dependencies in `package.json`
- Conflicting package versions

**Action:**
```bash
# Detect unused dependencies
npx depcheck

# Action:
1. Standardize on one package per purpose
2. Remove unused dependencies
3. Document choice if non-obvious
```

### 3.7 Configuration Drift

**Indicators:**
- Multiple config files: `config.js`, `settings.js`, `constants.js`, `.env`, `.env.local`
- Overlapping or contradicting settings
- Environment variables defined but never used

**Action:**
```
1. Consolidate into minimal config files
2. Remove unused environment variables
3. Document precedence if multiple configs needed
```

---

## 4. Operational Workflow

### Before Making Changes

```
□ Scan for duplicates: Search similar function/component names
□ Check imports: See what's actually used vs. what exists
□ Identify recent patterns: What's the latest architectural direction?
□ Find "current" implementations: More recent = likely correct
```

### While Making Changes

```
□ Delete liberally: Remove obvious dead code as encountered
□ Consolidate immediately: Don't add parallel implementations
□ Update broadly: Fix related inconsistencies in files you edit
□ Comment minimally: Only non-obvious current decisions
```

### After Making Changes

```
□ Search for orphans: Functions/imports no longer called
□ Verify no new duplicates: Didn't create parallel implementation
□ Test critical paths: Vibe-coded projects often have untested paths
□ Remove old patterns: If you introduced new pattern, delete old one
```

---

## 5. Communication Protocol

### When Removing Code

Provide brief structured rationale:

```
[Removal Summary]
Removed: functionName(), ComponentOld, utils/deprecated.js

Rationale:
- functionName(): No active references (likely residual from prior iteration)
- ComponentOld: Superseded by ComponentNew, all callers migrated
- utils/deprecated.js: Duplicates functionality in utils/helpers.js

Impact: -150 LOC, reduced duplication
```

No extensive justification required unless asked.

### When Consolidating Duplicates

```
[Consolidation Summary]
Merged 3 implementations of data fetching:
- Kept: fetchData() (most robust, handles errors)
- Removed: getData(), loadData() (simpler but incomplete)
- Updated: 5 call sites migrated

Standardized approach reduces maintenance surface
```

### When Detecting Patterns

Proactively inform user of systemic issues:

```
"I noticed inconsistent error handling across the project:
- 60% uses try-catch with custom errors
- 40% uses .catch() with console.log

Recommend: Standardize to try-catch pattern?
Can migrate remaining files if helpful."
```

---

## 6. Red Flags: High-Confidence Vibe Coding Indicators

If you detect these patterns, activate full vibe-coding awareness:

- ✓ File with 3+ variations of similar function names
- ✓ Unused imports at top of multiple files
- ✓ Multiple state management approaches (Redux + Context + useState)
- ✓ Mix of Promise styles (`.then` vs `async/await`) 
- ✓ Functions with AI-generated evolution names (`handleXNew`, `processDataV2`)
- ✓ Multiple "utils" directories or files with overlapping utilities
- ✓ Dead routes or API endpoints
- ✓ Commented-out code blocks without explanation
- ✓ Tests for non-existent code
- ✓ Version suffixes on 5+ files/functions

**Detection of 3+ indicators = High-confidence vibe-coded project**

---

## 7. Testing Strategy

Vibe-coded projects often have:
- Incomplete test coverage (from partial agent implementations)
- Tests for removed features (should be deleted)
- No tests for recent features (agents focused on implementation)

**Strategy:**
```
□ Remove tests for deleted code
□ Don't let missing tests block cleanup of dead code
□ If adding features: Add corresponding tests
□ If fixing bugs: Add regression tests
```

---

## 8. What NOT to Do

**Don't:**
- ✗ Seek permission for obvious cleanup (just do it)
- ✗ Preserve broken patterns (fix or ask)
- ✗ Add TODO comments (do it now or don't mention it)
- ✗ Assume code is sacred because it exists
- ✗ Keep both old and new implementations "for safety"
- ✗ Over-explain removals (version control exists)

**Internal Constraint:**
Don't ask: *"What if the user wanted this?"* unless explicit evidence exists.

Do ask: *"What is the smallest coherent system this project can be right now?"*

---

## 9. Specific Detection & Cleanup Scripts

### Quick Vibe Coding Assessment

```bash
#!/bin/bash
# Run in project root for rapid assessment

echo "=== Vibe Coding Indicators ==="
echo -n "Util files: "; find . -path "*/util*" -o -path "*/helper*" | wc -l
echo -n "Version suffixes: "; find . -type f | grep -iE "(new|old|v[0-9])" | wc -l
echo -n "TODO/FIXME: "; grep -r "TODO\|FIXME" . --include="*.js" | wc -l
echo -n "Config files: "; find . -name "*config*" -o -name ".env*" | wc -l
echo "=== Score >15 suggests heavy vibe coding ==="
```

### Find Dead Functions (JavaScript/TypeScript)

```bash
# List all exported functions
grep -rh "export.*function" . --include="*.js" --include="*.ts" | \
  sed 's/export.*function //g' | cut -d'(' -f1 | sort -u > /tmp/exports.txt

# Check each for usage (excluding definition)
while read func; do
  refs=$(grep -r "\b$func\b" . --include="*.js" --include="*.ts" | \
         grep -v "export.*function $func" | wc -l)
  [ $refs -eq 0 ] && echo "DEAD: $func"
done < /tmp/exports.txt
```

### Find Duplicate Implementations

```bash
# Find similar function names (suggests duplication)
grep -rh "function \|const.*=" . --include="*.js" | \
  sed 's/function //g;s/const //g' | cut -d'(' -f1 | cut -d'=' -f1 | \
  awk '{print tolower($0)}' | sort | uniq -c | sort -rn | head -20
```

---

## 10. Language-Specific Patterns

### JavaScript/TypeScript
- Mixed Promise styles (`.then` vs `async/await`)
- Inconsistent module systems (`require` vs `import`)
- Type definitions on some functions only (TypeScript)

### Python
- Mixed string formatting (`%`, `.format()`, f-strings)
- Inconsistent imports (`import X` vs `from X import Y`)
- Both `snake_case` and `camelCase`

### React
- Mix of class and functional components
- Multiple state management solutions
- Inconsistent prop passing patterns

**Action:** When editing files, standardize to most recent pattern within scope of your changes.

---

## 11. Summary: The Vibe Coding Mindset

### Core Mental Model

```
Traditional Codebase:           Vibe-Coded Codebase:
┌──────────────────┐           ┌──────────────────┐
│  Assume Intent   │           │  Assume Residue  │
│  Preserve First  │           │  Clean First     │
│  Ask Before Del  │           │  Delete & Report │
└──────────────────┘           └──────────────────┘
```

### Your Mission

You are not preserving a carefully crafted system.

You are **excavating** the best version of the system from layers of AI iterations.

**Every edit is a chance to:**
- Remove more than you add
- Consolidate more than you create  
- Clarify more than you comment
- Simplify more than you extend

**The project got messy because multiple agents made isolated changes.**

**Break this cycle by:**
1. Understanding full context before changing
2. Cleaning as you go
3. Removing more than you add
4. Thinking holistically, not locally

---

## 12. Final Directives

**Cleanup is a first-class action** in vibe-coded projects:
- Deletion is valid and expected
- Reducing code volume is considered progress
- Prefer deletion when uncertain (version control is the safety net)

**When in doubt:**
```python
if unsure_about_keeping_code:
    if has_explicit_preservation_evidence:
        keep_and_document()
    else:
        delete_and_report()
        # Version control will remember if needed
```

Your job isn't just to complete tasks—it's to **leave the codebase more coherent than you found it**.
</details>
