## Epic Workflow Prompt

The epic workflow prompt (`bmad-helper/prompts/epic-prompt.md`) is an autonomous AI agent workflow for executing complete epics from start to finish with minimal human intervention.

### Quick Start

To execute an epic, simply provide the epic number:

```
Execute Epic [EPIC_NUMBER]
```

**That's it!** The workflow will automatically:
- Find the next story to work on
- Generate necessary context
- Implement features
- Run tests and validations
- **Continue to the next story without stopping**
- Track progress through completion

**Important:** The workflow runs **continuously** through all stories. It will not pause or wait for confirmation between stories—only for critical blockers.

### How It Works

#### Prerequisites

Your project should have:
- `docs/epics/` folder with epic files named `epic-[N]-*.md`
- `docs/sprint-status.yaml` tracking story states
- Story files in `docs/stories/` (created automatically if missing)

#### Workflow Overview

The prompt executes a structured 8-step workflow **per story**:

1. **Story File Check** - Verifies story documentation exists, creates if missing
2. **Generate Context** - Creates story-specific context XML for implementation
3. **Start Work** - Updates sprint status from `backlog` → `drafted` → `in-progress`
4. **Implement** - Writes tests, implements features, handles edge cases
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

The workflow **auto-fixes without asking**:
- Linting/formatting errors
- Missing imports
- Type errors
- Flaky tests (retries up to 3x)
- Common file/path issues

Only **critical blockers** will interrupt for human input.

#### Validation Gates

Before marking any story complete, the workflow **MUST** create:

**Per-Story Validation Guide** (`docs/validation/epic[N]_[STORY_ID]_validation.md`):
- 30-second quick test
- Automated test results (unit, integration, coverage)
- Manual testing steps (exact commands, API calls, prompts)
- Edge cases and error handling tests
- Rollback plan
- Acceptance criteria checklist

**Epic Validation Guide** (`docs/validation/epic[N]_validation.md`):
- Created when all stories are complete
- Synthesizes all per-story guides
- End-to-end smoke test (30 seconds)
- Integration scenarios across stories
- Complete user journey testing

These guides ensure nothing is marked "done" without clear proof of completion.

### Token Management & Handoffs

#### Auto-Compaction

When token usage exceeds 190k, the workflow automatically:
1. Creates/updates `docs/handoff/epic[N]_handoff.md`
2. Saves complete progress snapshot
3. Notifies you to resume from handoff

#### Resuming Work

To continue from a handoff:

```
Resume Epic [N] from handoff
```

The workflow will:
1. Read the most recent handoff file
2. Load sprint status and current story context
3. Execute the exact next action
4. Continue seamlessly

### Progress Tracking

After each story completion, you'll see a progress report before the workflow **automatically continues to the next story**:

```
✅ Story [ID] done
Progress: [X/Y] stories ([Z]%)
Token Usage: [used]/200k
Next: Story [NEXT_ID]
```

**Note:** The workflow does **not** stop after this report. It immediately begins working on the next story.

### Epic Completion

When all stories are complete:

```
🎉 EPIC [N] COMPLETE

Stories: [Y/Y] ✓
Files Modified: [count]
Tests Added: [count]
Coverage: [avg %]
Validation Guides: docs/validation/epic[N]_*.md
Handoff: docs/handoff/epic[N]_handoff.md

Technical Debt: [list or none]
Ready for Epic [N+1]
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
│   └── epic-[N]-*.md                    # Epic specification
├── stories/
│   ├── [STORY_ID]-*.md                  # Story details
│   └── [STORY_ID]-*.context.xml         # Generated context
├── validation/
│   ├── epic[N]_[STORY_ID]_validation.md # Per-story validation
│   └── epic[N]_validation.md            # Epic-level validation
├── handoff/
│   └── epic[N]_handoff.md               # Progress snapshots
└── sprint-status.yaml                    # Story state tracking
```

### Example Usage

**Start an epic:**
```
Execute Epic 5
```

**The workflow will:**
- Create branch epic-5
- Find first story in backlog
- Generate context
- Implement with tests
- Create validation guide
- Move to next story WITHOUT STOPPING
- Continue autonomously until all stories complete

**If interrupted or tokens run high:**
```
Resume Epic 5 from handoff
```

### Best Practices

1. **Trust the Workflow** - Let it handle common issues autonomously
2. **Review Validation Guides** - These are your proof of completion
3. **Use Handoffs** - Don't fight token limits, embrace the handoff system
4. **Check Progress Reports** - Stay informed without micromanaging
5. **Interrupt Only for Blockers** - Let auto-fix handle routine issues

## Contributing

Contributions welcome! Please submit PRs with improvements to the workflow prompts.

## License

MIT
