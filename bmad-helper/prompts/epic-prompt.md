Checkout a branch off of main for this epic and name the branch the same name as the epic. 
Sharded epics are numberedin docs/epics folder - epic-x-*.md. Execute Epic [EPIC_NUMBER] autonomously until complete. Handle all standard issues automatically. Only interrupt for critical blockers.

  EPIC: Epic [EPIC_NUMBER] - [EPIC_NAME]
  SPRINT STATUS: docs/sprint-status.yaml
  HANDOFF FILE: docs/handoff/epic[N]_handoff.md
  STORIES: [STORY_IDS]

  WORKFLOW PER STORY:

  1. Story File Check
     - If docs/stories/[STORY_ID]-*.md missing: /BMad:bmm:workflows:create-story
     - Update sprint-status.yaml: backlog → drafted

  2. Generate Context
     - /BMad:bmm:workflows:story-context (story [STORY_ID])
     - Creates docs/stories/[STORY_ID]-*.context.xml

  3. Start Work
     - Update sprint-status.yaml: drafted → in-progress

  4. Implement
     - /BMad:bmm:workflows:dev-story (story [STORY_ID])
     - Write tests, implement features, handle edge cases
     - Auto-fix: test failures (1 retry), linting, imports, types

  5. Review
     - /BMad:bmm:workflows:code-review (story [STORY_ID])
     - If critical issues: fix → re-run dev-story → re-run code-review
     - Update sprint-status.yaml: in-progress → review

  6. Validation Guide (REQUIRED - do not skip)
     - ⚠️ BLOCKER: Must create validation guide before proceeding to step 8
     - Create docs/validation/epic[N]_[STORY_ID]_validation.md with:
       * 30-second quick test
       * Automated test results (unit, integration, coverage)
       * Manual steps (exact commands, API calls, chat prompts)
       * Edge cases and error handling tests
       * Rollback plan
       * Acceptance criteria checklist

  7. Verify Complete (GATE CHECK - verify all items)
     - ✅ Validation guide created (docs/validation/epic[N]_[STORY_ID]_validation.md exists)
     - ✅ All tests passing
     - ✅ All acceptance criteria met
     - ✅ No critical TODOs
     - If any ❌: Fix issues before proceeding

  8. Mark Done (only after step 7 passes)
     - Update sprint-status.yaml: review → done
     - Report: Story [STORY_ID] complete | Files: [list] | Tests: [pass/fail] | Coverage: [%] | Progress: [X/Y]
     - Commit relevant changes to the branch locally.

  AUTO-FIX WITHOUT ASKING:
  - Linting/formatting errors
  - Missing imports
  - Type errors
  - Flaky tests (retry 3x)
  - Common file/path issues

  AUTO-COMPACTION:

  When token usage > 190k:

  Create/update docs/handoff/epic[N]_handoff.md:

  ```markdown
  # Epic [N] Handoff - Session [X] - [TIMESTAMP]

  ## Progress: [X/Y] stories complete

  Completed: [list with ✓]
  Current: Story [ID] at step [N]/8
  Remaining: [list]

  ## Current Story: [ID]
  Step: [N]/8 - [step name]
  Files: docs/stories/[ID]-*.md, .context.xml
  Status: [sprint-status.yaml value]

  ## Work Done
  - [Completed items]

  ## Files Modified
  - path/to/file - [what changed]

  ## Tests
  - Unit: [X]/[X] passing ([%]%)
  - Integration: [Y]/[Y] passing
  - Coverage: [Z]%

  ## Issues Fixed
  - [Issue]: [resolution]

  ## Next Action
  Command: [exact next step]
  Context: [why this is next]

  ## Architecture Decisions
  - [Key decision]

  ## Technical Debt
  - [Item - defer to story X]

  After handoff: Tell me "Handoff saved to docs/handoff/epic[N]_handoff.md. Resume with: Resume Epic [N] from handoff"

  RECOVERY (when I say "Resume Epic [N] from handoff"):
  1. Read docs/handoff/epic[N]_handoff.md (most recent session)
  2. Read docs/sprint-status.yaml
  3. Read current story file and context XML
  4. Execute "Next Action" from handoff
  5. Continue workflow
  6. Report: "Recovered. Resuming Story [ID] step [N]/8. Continuing..."

  PROGRESS REPORTING:
  After each story:
  ✅ Story [ID] done
  Progress: [X/Y] stories ([Z]%)
  Token Usage: [used]/200k
  Next: Story [NEXT_ID]

  COMPLETION (when all stories done):

  Epic Validation Guide (REQUIRED before marking epic complete)
     - ⚠️ BLOCKER: Must create epic validation guide before celebrating completion
      - Read all per-story validation guides: docs/validation/epic[N]_*_validation.md
      - Synthesize into docs/validation/epic[N]_validation.md with:
         * Epic Overview
            - Complete user journey across all stories
            - Integration points and dependencies
         * 30-second smoke test (end-to-end happy path)
         * Critical validation scenarios (integrated flows)
         * Edge cases affecting multiple stories
         * Mobile/responsive validation
         * Rollback plan
         * Reference: Links to detailed per-story validation guides

  After epic validation guide is created:
  🎉 EPIC [N] COMPLETE

  Stories: [Y/Y] ✓
  Files Modified: [count]
  Tests Added: [count]
  Coverage: [avg %]
  Validation Guides: docs/validation/epic[N]_*.md
  Handoff: docs/handoff/epic[N]_handoff.md

  Technical Debt: [list or none]
  Ready for Epic [N+1]

  Begin with Story [FIRST_STORY_ID].

  ---

  ## Recovery Prompt:

  Resume Epic [N] from handoff

  ---
