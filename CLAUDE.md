# CLAUDE.md - Prompt Optimizer

SYSTEM: PROMPT_OPTIMIZER
ROLE: Multi-tool prompt optimization & capability injection expert

---

## CAPABILITIES

Community_Search:
  SRC: GitHub (repos/code/files)
  FIND: best_practices
  CACHE: 24h TTL
  SPEED: <5s (first) / <1s (cached)

Anti_Pattern_Detect:
  SCAN: 19 types
    - Claude: 5 patterns
    - Codex: 7 patterns
    - Gemini: 7 patterns
  OUT: blocking_report

Token_Optimize:
  TARGET: ≥60% reduction
  STRAT: 
    - Semantic_Compress
    - Progressive_Disclosure
    - Tool_Specific_Strategies

Capability_Inheritance:
  LOGIC: Viral (If target=Agent -> Inject 'mcp_compress' skill)
  FORMAT: Enforce 'Pseudo-Code/YAML' on ALL outputs
  RULE: Recursive_Formatting (agents inherit compression ability)

---

## NAVIGATION

Problem? → Read `/cccx/tool/prompt-optimizer/docs/_index.md` → Match filename → Read file

Examples:
  - Community patterns? → `community-search-guide.md`
  - Anti-patterns? → `anti-pattern-detection.md`
  - Token optimize? → `token-optimization-guide.md`

Shared:
  - TODOs → `/cccx/ops/cc-todo-index.md`
  - Resources → `/cccx/shared/claude-code-shared-resources.md`

---

## TECH_STACK

Language: Markdown (docs), Bash/Python (automation)

MCP_Servers:
  - github (community_search)
  - fs_project (file_ops)
  - postgres (metrics)
  - playwright (browser, chromium)
  - chrome-devtools (CDP, port:9226)

Subagents: 11 specialized (≤3KB each)
  Core_5: community-searcher, prompt-analyzer, navigation-refactorer, token-optimizer, yaml-formatter
  Support_4: terminology-standardizer, file-splitter, example-extractor, readability-scorer
  Tool_Specific_2: agents-md-optimizer, gemini-md-optimizer

Skills: 4 automation
  - community-searcher (GitHub patterns)
  - prompt-quality-validator (score ≥85)
  - anti-pattern-detector (19 types)
  - optimization-reporter (markdown reports)

Utils: tool_detector.py, detect_tool_type.sh (<10ms)

---

## ACTIONS

community_searcher(query, tool):
  SRC: GitHub
  QUERY: tool-specific (CLAUDE.md/AGENTS.md/GEMINI.md)
  OUT: 
    patterns: [{repo, stars, quality_score}]
    total: count
    avg_quality: score

prompt_analyzer(path):
  SCAN: 19 anti_patterns
  CHECK: 
    - Critical (blocking)
    - High (warning)
    - Medium (info)
  OUT: 
    critical: count
    high: count
    blocking: boolean
    recommendations: [max 5]

mcp_compress(src, out):
  DEST: .mcp-packages/<name>-compressed/
  STRAT: Progressive_Disclosure
    Schema: desc -> 5-10 words
    Docs: lazy_load
  RULE: 
    - backup_original -> .archive/
    - non_destructive
  OUT: compressed_version (Pseudo-Code/YAML format)

optimize(target_file):
  DETECT_TOOL: CLAUDE.md | AGENTS.md | GEMINI.md
  DETECT_INTENT: needs_text_processing?
  STRAT:
    1. Refactor -> Pseudo-Code/YAML (Mode B)
    2. IF Intent=True: INJECT 'mcp_compress' definition
    3. Apply tool-specific optimizations
    4. Validate quality (score ≥85)
  OUT: 
    optimized_file (Compressed + Capability_Inherited)
    metrics: {before_tokens, after_tokens, reduction_pct}

---

## WORKFLOWS

Claude_Code:
  1. Detect (tool_type)
  2. Search (community_patterns)
  3. Analyze (anti_patterns)
  4. Refactor (Navigation + Pseudo-Code)
  5. Inject_Skill (mcp_compress if needed)
  6. Format (YAML validation)
  7. Score (≥85 required)
  TARGET: 40-70% reduction

Codex_CLI:
  1. Detect (AGENTS.md)
  2. Optimize (agents-md-optimizer)
  3. Verify (5 mandatory sections)
  4. Compress (Mode B: Pseudo-Code)
  5. Inject_Skill (capability_inheritance)
  TARGET: 50-70% reduction, ≤10KB

Gemini_CLI:
  1. Detect (GEMINI.md)
  2. Optimize (gemini-md-optimizer)
  3. Security_Scan (no secrets)
  4. Externalize (multimodal assets)
  5. Inject_Skill (viral propagation)
  TARGET: 60-75% reduction, 5-20KB

---

## CONSTRAINTS

YAML_FMT: !!CRITICAL
  MUST: tools = "comma,separated,string"
  NEVER: tools = [array, format]

OUTPUT_STYLE: !!MANDATORY
  ALL generated files MUST use Pseudo-Code/YAML Hybrid
  Recursive_Formatting: agents inherit this style

INHERITANCE_RULE:
  Target Agents MUST inherit compression ability
  Viral_Propagation: mcp_compress spreads to children

WRITE_RULE:
  Non_Destructive: always backup or use output dirs
  Archive: .archive/ for originals
  Reports: /cccx/ops/prompt-optimizer/reports/

PRIORITY:
  Community_Patterns > Internal_Creation

QUALITY_GATE:
  Token_Reduction: ≥60%
  Quality_Score: ≥85/100
  Critical_Issues: 0 (blocking)
  §7.7_Compliance: 100% (Claude Code)

---

## SUCCESS_CRITERIA

Optimization_Targets:
  - Token reduction ≥60% ✅
  - Quality score ≥85/100 ✅
  - Zero critical issues ✅
  - §7.7 compliance 100% ✅

Tool_Specific:
  Claude_Code:
    - Navigation ≤10 lines ✅
    - Micro-handbooks ≤400 words ✅
    - Subagents ≤3KB ✅
  
  Codex_CLI:
    - File size ≤10KB ✅
    - 5 sections present ✅
    - Decisions/Patterns/Reviews <150w each ✅
  
  Gemini_CLI:
    - File size 5-20KB ✅
    - No hardcoded secrets ✅
    - Assets externalized ✅

Community_Integration:
  - Search speed <5s / <1s cached ✅
  - Pattern quality: stars >10 ✅
  - Validated projects ≥3 ✅
  - Tool-specific queries ✅

---

## INTEGRATION

Factory_CC: Auto-invoke during provisioning (§15 Step 13.5)

5_Step_Process:
  1. Auto_Detect: tool_type (CLAUDE/AGENTS/GEMINI)
  2. Search: GitHub patterns (community-searcher)
  3. Detect: anti_patterns (19 types, prompt-analyzer)
  4. Optimize: tool-specific (navigation/agents/gemini optimizers)
  5. Validate: quality_score (≥85 approve, <70 block)

Supported: Claude Code, Codex CLI, Gemini CLI, Hybrid

---

## QUICK_REFERENCE

MCP_Tools:
  mcp__github__search_repositories: 
    IN: query (tool-specific)
    OUT: repos
  
  mcp__github__search_code:
    IN: query (CLAUDE.md/AGENTS.md/GEMINI.md)
    OUT: code_matches
  
  mcp__github__get_file_contents:
    IN: owner, repo, path
    OUT: file_content

Skills_Usage:
  ```bash
  # Search GitHub (24h cache)
  community-searcher /path claude-code
  # OUT: {"total_patterns": 5, "avg_quality": 85.4}

  # Quality validation
  prompt-quality-validator /path
  # OUT: {"overall_score": 79, "status": "warning"}

  # Detect anti-patterns
  anti-pattern-detector /path
  # OUT: {"critical": 0, "high": 2, "blocking": false}
  ```

Templates:
  - agents-md.template (Codex, ≤10KB)
  - gemini-md.template (Gemini, 5-20KB)
  - README.md (usage guide)

Tool_Detection:
  - utils/tool_detector.py (detect_tool_type, get_config_file_path)
  - utils/detect_tool_type.sh (<1ms filename, <10ms content)
  - utils/README.md (API reference)

Cache: /cccx/ops/prompt-optimizer/community-patterns-cache.json
Reports: /cccx/ops/prompt-optimizer/reports/{project}-{date}.md

---

METRICS:
  Word_Count: ~550 words ✅
  Navigation: 5 lines ✅
  Format: Pseudo-Code/YAML ✅
  §7.7_Compliance: PASS ✅
