## Epic Workflow Prompt

> **⚠️ Work in Progress**
>
> This is a personal workflow I'm developing to execute epics faster. I'm still learning about BMAD (Business Model and Design) methodology and actively experimenting to discover what works best. This workflow is evolving as I learn and iterate on my process.

The epic workflow prompt (`bmad-helper/prompts/epic-prompt.md`) is an autonomous AI agent workflow for executing complete epics from start to finish with minimal human intervention.

### Quick Start

To execute an epic, provide the epic ID and prompt file:

```
Execute Epic [EPIC_ID] following epic-prompt.md
```

**That's it!** The workflow will automatically:
- Find the next story to work on
- Generate necessary context
- Implement features
- Run tests and validations
- **Continue to the next story without stopping**
- Track progress through completion

**Important:** The workflow runs **continuously** through all stories. It will not pause or wait for confirmation between stories—only for critical blockers.

### Placeholder Reference

The workflow uses descriptive placeholders throughout:

| Placeholder | Meaning |
|-------------|---------|
| `[EPIC_ID]` | The epic identifier |
| `[EPIC_NAME]` | Name of the epic |
| `[STORY_ID]` | Current story identifier |
| `[STORY_IDS]` | List of all story IDs in the epic |
| `[NEXT_STORY_ID]` | Next story to work on |
| `[FIRST_STORY_ID]` | First story in the epic |
| `[COMPLETED_COUNT]` | Number of completed stories |
| `[TOTAL_STORIES]` | Total number of stories in epic |
| `[PERCENTAGE]` | Percentage value |
| `[AVERAGE_PERCENTAGE]` | Average percentage across stories |
| `[CURRENT_TOKENS]` | Current token usage |
| `[COUNT]` | Generic count value |
| `[SESSION_NUMBER]` | Handoff session number |
| `[STEP_NUMBER]` | Current step (1-8) in workflow |
| `[PASSING]` | Number of passing tests |
| `[TOTAL]` | Total number of tests |
| `[TIMESTAMP]` | Date and time stamp |

### How It Works

#### Prerequisites

Your project should have:
- `docs/epics/` folder with epic files named `epic-[EPIC_ID]-*.md`
- `docs/sprint-status.yaml` tracking story states
- Story files in `docs/stories/` (created automatically if missing)

#### Workflow Overview

The prompt executes a structured 8-step workflow **per story**:

1. **Story File Check** - Verifies story documentation exists, creates if missing, updates status `backlog` → `drafted`
2. **Generate Context** - Creates story-specific context XML for implementation
3. **Start Work** - Updates sprint status from `drafted` → `in-progress`
4. **Implement** - Writes tests, implements features, handles edge cases, auto-fixes test failures (retry 3x)
5. **Review** - Performs code review, fixes critical issues
6. **Validation Guide** - Creates detailed testing documentation (REQUIRED gate)
7. **Verify Complete** - Gate check ensuring all criteria met before proceeding
8. **Mark Done** - Updates status to `done`, commits changes, reports progress, **immediately continues to next story**

#### Story State Flow

```
backlog → drafted → in-progress → review → done
```

States are tracked in `docs/sprint-status.yaml`.

#### Autonomous Problem Solving

The workflow **auto-fixes without asking** (retries up to 3x for all types):
- **Linting/formatting errors** - Deterministic fixes (add semicolons, fix indentation)
- **Missing imports** - Adds required import statements
- **Type errors** - Fixes type mismatches and cascading type issues
- **Test failures** - Attempts to fix code logic that causes test failures
- **Flaky tests** - Re-runs tests that intermittently pass/fail to verify reliability
- **Common file/path issues** - Resolves file not found and path errors

**How retries work:**
- Each auto-fix type gets up to 3 retry attempts
- For code issues (types, tests): Each retry includes fixing the code and re-running
- For flaky tests: Each retry re-runs the same code to detect intermittent failures
- Simple fixes (linting, imports) typically succeed on first attempt

Only **critical blockers** that cannot be auto-fixed after 3 retries will interrupt for human input.

#### Validation Gates

Before marking any story complete, the workflow **MUST** create:

**Per-Story Validation Guide** (`docs/validation/epic[EPIC_ID]_[STORY_ID]_validation.md`):
- 30-second quick test
- Automated test results (unit, integration, coverage)
- Manual testing steps (exact commands, API calls, chat prompts)
- Edge cases and error handling tests
- Rollback plan
- Acceptance criteria checklist

**Epic Validation Guide** (`docs/validation/epic[EPIC_ID]_validation.md`):
- Created when all stories are complete
- Synthesizes all per-story guides
- End-to-end smoke test (30 seconds)
- Integration scenarios across stories
- Complete user journey testing

These guides ensure nothing is marked "done" without clear proof of completion.

### Token Management & Handoffs

#### Auto-Compaction

When token usage exceeds 190k, the workflow automatically:
1. Creates/updates `docs/handoff/epic[EPIC_ID]_handoff.md`
2. Saves complete progress snapshot
3. Notifies you to resume from handoff

#### Resuming Work

To continue from a handoff:

```
Resume Epic [EPIC_ID] from handoff using epic-prompt.md
```

**How recovery works:**
- The epic-prompt.md file contains a RECOVERY section that defines what "from handoff" means
- When you use this phrase, the AI reads the prompt and follows the recovery instructions
- The prompt is self-documenting - it defines its own recovery behavior

The workflow will:
1. Read the most recent handoff file
2. Load sprint status and current story context
3. Execute the exact next action
4. Continue seamlessly

### Progress Tracking

After each story completion, you'll see a progress report before the workflow **automatically continues to the next story**:

```
✅ Story [STORY_ID] done
Progress: [COMPLETED_COUNT]/[TOTAL_STORIES] stories ([PERCENTAGE]%)
Token Usage: [CURRENT_TOKENS]/200k
Next: Story [NEXT_STORY_ID]
```

**Note:** The workflow does **not** stop after this report. It immediately begins working on the next story.

### Epic Completion

When all stories are complete:

```
🎉 EPIC [EPIC_ID] COMPLETE

Stories: [TOTAL_STORIES]/[TOTAL_STORIES] ✓
Files Modified: [COUNT]
Tests Added: [COUNT]
Coverage: [AVERAGE_PERCENTAGE]%
Validation Guides: docs/validation/epic[EPIC_ID]_*.md
Handoff: docs/handoff/epic[EPIC_ID]_handoff.md

Technical Debt: [list or none]
Ready for next epic
```

### Key Features

✅ **Fully Autonomous** - Runs complete epics without constant supervision
✅ **Continuous Execution** - Works through all stories without stopping between them
✅ **Self-Healing** - Auto-fixes common issues (linting, imports, types, flaky tests)
✅ **Structured Gates** - Validation guides prevent premature completion
✅ **Session Recovery** - Handoff system enables pause/resume across sessions
✅ **Progress Transparency** - Clear reporting at each story completion
✅ **Quality Enforcement** - Code review, test coverage, acceptance criteria checks

### File Structure After Execution

```
docs/
├── epics/
│   └── epic-[EPIC_ID]-*.md                         # Epic specification
├── stories/
│   ├── [STORY_ID]-*.md                             # Story details
│   └── [STORY_ID]-*.context.xml                    # Generated context
├── validation/
│   ├── epic[EPIC_ID]_[STORY_ID]_validation.md      # Per-story validation
│   └── epic[EPIC_ID]_validation.md                 # Epic-level validation
├── handoff/
│   └── epic[EPIC_ID]_handoff.md                    # Progress snapshots
└── sprint-status.yaml                               # Story state tracking
```

### Example Usage

**Start an epic:**
```
Execute Epic 5 following epic-prompt.md
```
Provide file path of epic-prompt.md which is in a common non-project directory, so the prompt modifications persist across projects.

**The workflow will:**
- Create branch epic-[EPIC_ID]-[EPIC_NAME]
- Find first story in backlog
- Generate context
- Implement with tests
- Create validation guide
- Move to next story WITHOUT STOPPING
- Continue autonomously until all stories complete

**If interrupted or tokens run high:**
```
Resume Epic 5 from handoff following epic-prompt.md
```

### Strategy

1. **Trust the Workflow** - Let it handle common issues autonomously
2. **Review Validation Guides** - These are for your manual validation
3. **Use Handoffs** - Handoffs are meant to pre-emptively prepare and be ready for compaction.
4. **Check Progress Reports** - Stay informed without needing to be present all the time.
5. **Interrupt Only for Blockers** - Let auto-fix handle routine issues

## Contributing

Contributions welcome! Please submit PRs with improvements to the workflow prompts.

## License

MIT
