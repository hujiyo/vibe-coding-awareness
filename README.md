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
