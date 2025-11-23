# CLAUDE.md - Prompt Optimizer

**Project**: prompt-optimizer
**Version**: 1.0
**Status**: ACTIVE

---

## Overview

Prompt Optimizer是一个**多工具支持的提示词优化Project CC**，支持Claude Code (CLAUDE.md)、Codex CLI (AGENTS.md)、Gemini CLI (GEMINI.md)三种AI工具。通过主动搜索GitHub社区最佳实践、检测工具特定anti-patterns、应用验证优化模式，实现60-70% token reduction。

**核心能力**:
- **多工具支持**: Claude Code, Codex CLI, Gemini CLI三工具覆盖
- 主动社区搜索（GitHub repos/code/files，工具特定查询）
- Anti-pattern检测（19个已知问题：5 Claude + 7 Codex + 7 Gemini）
- Token效率优化（语义保留压缩，工具特定策略）
- 自动工具检测（文件名 + 内容heuristic，<10ms）
- 模板化创建（agents-md.template, gemini-md.template）

---

## Navigation Method

遇到问题？打开 `/cccx/tool/prompt-optimizer/docs/_index.md` 看文件列表，找到文件名匹配的，读它。

**核心示例**:
- 需要搜索社区模式？ → \`community-search-guide.md\`
- 需要检测anti-patterns？ → \`anti-pattern-detection.md\`
- 需要优化token效率？ → \`token-optimization-guide.md\`

**其他问题类推**：看文件名，读对应文件。

**📋 Shared Resources**:
- Long-term TODOs? → \`/cccx/ops/cc-todo-index.md\`
- All shared resources? → \`/cccx/shared/claude-code-shared-resources.md\`

---

## Tech Stack

- **Language**: Markdown (documentation), Bash/Python (skills automation, tool detection)
- **MCP Servers**:
  - github (community search)
  - fs_project (file operations)
  - postgres (metrics storage)
  - playwright (browser automation, chromium)
  - chrome-devtools (Chrome DevTools Protocol, port 9226)
- **Subagents**: 11 specialized experts (Lean Mode, ≤3KB each) - Claude/Codex/Gemini support
- **Skills**: 4 automation tools (community search, validation, detection, reporting)
- **Utilities**: tool_detector.py, detect_tool_type.sh (auto-detect CLAUDE.md/AGENTS.md/GEMINI.md)

---

## Project Constraints

1. **§7.7 Mandatory**: 100% Golden Path compliance required
2. **Community-First**: Prioritize GitHub patterns over internal creation
3. **Token Threshold**: ≥60% reduction target for all optimizations
4. **Quality Gate**: ≥85/100 score for handoff approval
5. **YAML Format**: tools field must be comma-separated string (NOT array)

\`\`\`yaml
# ✅ Correct YAML Format
---
name: community-searcher
description: Search GitHub for optimization patterns
tools: Read, mcp__github__search_repositories, mcp__github__search_code
---

# ❌ Incorrect YAML Format (DO NOT USE)
---
tools: [Read, mcp__github__search_repositories]  # Array causes parse errors!
---
\`\`\`

---

## Subagent Usage

**11 Specialized Subagents** (Lean Mode ≤3KB):
- **Core 5** (Critical): community-searcher, prompt-analyzer, navigation-refactorer, token-optimizer, yaml-formatter
- **Support 4** (High): terminology-standardizer, file-splitter, example-extractor, readability-scorer
- **Tool-Specific 2**: agents-md-optimizer (Codex CLI), gemini-md-optimizer (Gemini CLI)

**Invocation Methods**:
- **Automatic**: 描述任务，Claude自动匹配subagent
- **Explicit**: Direct invocation with task description
- **Tool-aware**: Context-sensitive optimization

\`\`\`python
# Example: Optimize a Codex CLI AGENTS.md file
agents-md-optimizer(
    "Optimize /cccx/tool/my-project/AGENTS.md for 60-70% token reduction"
)

# Example: Search GitHub for community patterns
community-searcher(
    "Find navigation optimization patterns for CLAUDE.md"
)

# Example: Detect anti-patterns before handoff
prompt-analyzer(
    "Scan /cccx/tool/my-project for all anti-patterns"
)
\`\`\`

---

## Typical Workflow

**Complete workflow examples have been externalized for better maintainability.**

📖 **Full Workflows**: [\`/cccx/tool/prompt-optimizer/docs/guides/workflow-examples.md\`](/cccx/tool/prompt-optimizer/docs/guides/workflow-examples.md)

**Three Workflows** (类比: 工厂流水线):
- **Claude Code**: 检测 → 社区搜索 → 分析 → 重构导航 → 格式 → 评分 (40-70% reduction, score ≥85)
- **Codex CLI**: 检测 → 优化器 → 验证5段 → 压缩 → 评分 (50-70% reduction, ≤10KB)
- **Gemini CLI**: 检测 → 优化器 → 安全扫描 → 外部化资产 → 评分 (60-75% reduction, no secrets)

📖 **详细流程**: \`/cccx/tool/prompt-optimizer/docs/guides/workflow-examples.md\`

---

## Testing Environments

**Testing**: lab-01 (基础), lab-02 (完整验证平台)⭐ → 📖 \`/cccx/docs/testing-labs.md\`

---

## Success Criteria

**Optimization Targets** (通用所有工具):
- ✅ Token reduction ≥60%
- ✅ §7.7 compliance 100% (Claude Code)
- ✅ Quality score ≥85/100
- ✅ Zero Critical issues at handoff

**Tool-Specific Targets**:
- **Claude Code (CLAUDE.md)**:
  - ✅ Navigation ≤10 lines (§7.7 Template 1)
  - ✅ Micro-handbooks ≤400 words
  - ✅ Subagent configs ≤3KB (Lean Mode)
- **Codex CLI (AGENTS.md)**:
  - ✅ File size ≤10KB (~2,500 words)
  - ✅ 5 mandatory sections present
  - ✅ Decisions/Patterns/Reviews <150 words each
- **Gemini CLI (GEMINI.md)**:
  - ✅ File size 5-20KB (optimal: 2,000-3,000 words)
  - ✅ No hardcoded secrets (security scan passed)
  - ✅ Multimodal assets externalized (no base64)

**Community Integration**:
- ✅ Search speed <5秒（首次），<1秒（缓存命中）
- ✅ Pattern quality: stars >10, validated_projects ≥3
- ✅ 24h cache TTL（避免频繁API调用）
- ✅ Tool-specific queries (CLAUDE.md, AGENTS.md, GEMINI.md patterns)

**Reporting Standards**:
- ✅ Before/after metrics mandatory
- ✅ Community sources attribution
- ✅ Recommendations ≤5条
- ✅ Archive retention 12 months

---

## Integration with Factory CC

**Prompt-optimizer can be invoked automatically during Factory CC provisioning** (Factory CC §15 Step 13.5):

**5-Step Process**:
1. Auto-detect tool type (CLAUDE.md/AGENTS.md/GEMINI.md)
2. Search GitHub for tool-specific patterns (community-searcher)
3. Detect anti-patterns (19 types across 3 tools via prompt-analyzer)
4. Apply tool-specific optimizations (navigation-refactorer, agents-md-optimizer, gemini-md-optimizer)
5. Validate quality score (readability-scorer: score ≥85 = handoff approved, <70 = blocked)

**Supported**: Claude Code, Codex CLI, Gemini CLI, Hybrid projects (multiple config files)

---

## Quick Reference

**MCP Tools**:
- \`mcp__github__search_repositories\`: 搜索repos (工具特定查询)
- \`mcp__github__search_code\`: 搜索代码 (CLAUDE.md/AGENTS.md/GEMINI.md)
- \`mcp__github__get_file_contents\`: 读取文件内容

\`\`\`python
# Example: Search GitHub for navigation patterns
mcp__github__search_code(
    q="navigation section CLAUDE.md",
    per_page=5
)

# Example: Get community pattern file
mcp__github__get_file_contents(
    owner="anthropics",
    repo="claude-code-examples",
    path="patterns/navigation-template.md"
)
\`\`\`

**Skills**:
- \`community-searcher\`: 搜索GitHub优化模式 (24h cache, <5s首次/<1s缓存)
- \`prompt-quality-validator\`: 自动化质量评分 (3工具支持)
- \`anti-pattern-detector\`: 扫描19种已知问题 (5 Claude + 7 Codex + 7 Gemini)
- \`optimization-reporter\`: 生成markdown报告

\`\`\`bash
# Search GitHub for community patterns (cached 24h)
community-searcher /cccx/tool/my-project claude-code
# Output: {"total_patterns": 5, "average_quality_score": 85.4, ...}

# Run quality validation (returns JSON score)
prompt-quality-validator /cccx/tool/my-project
# Output: {"overall_score": 79, "status": "warning", ...}

# Detect anti-patterns before handoff
anti-pattern-detector /cccx/tool/my-project
# Output: {"critical": 0, "high": 2, "blocking": false}
\`\`\`

**Templates**:
- \`/cccx/tool/prompt-optimizer/templates/agents-md.template\` (Codex CLI, ≤10KB)
- \`/cccx/tool/prompt-optimizer/templates/gemini-md.template\` (Gemini CLI, 5-20KB)
- \`/cccx/tool/prompt-optimizer/templates/README.md\` (使用指南)

**Tool Detection**:
- \`utils/tool_detector.py\`: Python module (detect_tool_type, get_config_file_path)
- \`utils/detect_tool_type.sh\`: Bash wrapper (<1ms filename, <10ms content)
- \`utils/README.md\`: API reference and integration examples

**Cache Location**:
- \`/cccx/ops/prompt-optimizer/community-patterns-cache.json\` (24h TTL)

**Reports Archive**:
- \`/cccx/ops/prompt-optimizer/reports/{project}-{date}.md\`

---

---

**Word Count**: ~650 words ✅
**Navigation**: 5 lines ✅
**§7.7 Compliance**: ✅ Pass
