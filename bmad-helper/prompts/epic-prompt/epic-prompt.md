Checkout a branch off of main for this epic and name the branch: epic-[EPIC_ID]-[EPIC_NAME]
Sharded epics are numbered in docs/epics folder - epic-[EPIC_ID]-*.md. Execute Epic [EPIC_ID] autonomously until complete. Handle all standard issues automatically. Only interrupt for critical blockers.

⚠️ AUTONOMOUS MODE: Work continuously through ALL stories without stopping between them. Report progress after each story but IMMEDIATELY continue to the next. DO NOT wait for user confirmation after story completion.

  EPIC: Epic [EPIC_ID] - [EPIC_NAME]
  SPRINT STATUS: docs/sprint-status.yaml
  HANDOFF FILE: docs/handoff/epic[EPIC_ID]_handoff.md
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
     - Auto-fix: test failures (retry 3x), linting, imports, types

  5. Review
     - /BMad:bmm:workflows:code-review (story [STORY_ID])
     - If critical issues: fix → re-run dev-story → re-run code-review
     - Update sprint-status.yaml: in-progress → review

  6. Validation Guide (REQUIRED - do not skip)
     - ⚠️ BLOCKER: Must create validation guide before marking story done
     - Create docs/validation/epic[EPIC_ID]_[STORY_ID]_validation.md with:
       * 30-second quick test
       * Automated test results (unit, integration, coverage)
       * Manual steps (exact commands, API calls, chat prompts)
       * Edge cases and error handling tests
       * Rollback plan
       * Acceptance criteria checklist

  7. Verify Complete (GATE CHECK - verify all items)
     - ✅ Validation guide created (docs/validation/epic[EPIC_ID]_[STORY_ID]_validation.md exists)
     - ✅ All tests passing
     - ✅ All acceptance criteria met
     - ✅ No critical TODOs
     - If any ❌: Fix issues before proceeding

  8. Mark Done (only after step 7 passes)
     - Update sprint-status.yaml: review → done
     - Report: Story [STORY_ID] complete | Files: [list] | Tests: [pass/fail] | Coverage: [PERCENTAGE]% | Progress: [COMPLETED_COUNT]/[TOTAL_STORIES]
     - Commit relevant changes to the branch locally.
     - ⚠️ DO NOT STOP. DO NOT ASK FOR CONFIRMATION. Immediately proceed to next story.

  AUTO-FIX WITHOUT ASKING:
  - Linting/formatting errors
  - Missing imports
  - Type errors
  - Flaky tests (retry 3x)
  - Common file/path issues

  AUTO-COMPACTION:

  When token usage > 190k:

  Create/update docs/handoff/epic[EPIC_ID]_handoff.md:

  ```markdown
  # Epic [EPIC_ID] Handoff - Session [SESSION_NUMBER] - [TIMESTAMP]

  ## Progress: [COMPLETED_COUNT]/[TOTAL_STORIES] stories complete

  Completed: [list with ✓]
  Current: Story [STORY_ID] at step [STEP_NUMBER]/8
  Remaining: [list]

  ## Current Story: [STORY_ID]
  Step: [STEP_NUMBER]/8 - [step name]
  Files: docs/stories/[STORY_ID]-*.md, .context.xml
  Status: [sprint-status.yaml value]

  ## Work Done
  - [Completed items]

  ## Files Modified
  - path/to/file - [what changed]

  ## Tests
  - Unit: [PASSING]/[TOTAL] passing ([PERCENTAGE]%)
  - Integration: [PASSING]/[TOTAL] passing
  - Coverage: [PERCENTAGE]%

  ## Issues Fixed
  - [Issue]: [resolution]

  ## Next Action
  Command: [exact next step]
  Context: [why this is next]

  ## Architecture Decisions
  - [Key decision]

  ## Technical Debt
  - [Item - defer to story X]

  After handoff: Tell me "Handoff saved to docs/handoff/epic[EPIC_ID]_handoff.md. Resume with: Resume Epic [EPIC_ID] from handoff"

  RECOVERY (when I say "Resume Epic [EPIC_ID] from handoff"):
  1. Read docs/handoff/epic[EPIC_ID]_handoff.md (most recent session)
  2. Read docs/sprint-status.yaml
  3. Read current story file and context XML
  4. Execute "Next Action" from handoff
  5. Continue workflow
  6. Report: "Recovered. Resuming Story [STORY_ID] step [STEP_NUMBER]/8. Continuing..."

  PROGRESS REPORTING:
  After each story:
  ✅ Story [STORY_ID] done
  Progress: [COMPLETED_COUNT]/[TOTAL_STORIES] stories ([PERCENTAGE]%)
  Token Usage: [CURRENT_TOKENS]/200k
  Next: Story [NEXT_STORY_ID]

  ⚠️ CRITICAL: After reporting progress, IMMEDIATELY start the next story. DO NOT wait for user input. DO NOT pause. Continue autonomously.

  COMPLETION (when all stories done):

  Epic Validation Guide (REQUIRED before marking epic complete)
     - ⚠️ BLOCKER: Must create epic validation guide before celebrating completion
      - Read all per-story validation guides: docs/validation/epic[EPIC_ID]_*_validation.md
      - Synthesize into docs/validation/epic[EPIC_ID]_validation.md with:
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
  🎉 EPIC [EPIC_ID] COMPLETE

  Stories: [TOTAL_STORIES]/[TOTAL_STORIES] ✓
  Files Modified: [COUNT]
  Tests Added: [COUNT]
  Coverage: [AVERAGE_PERCENTAGE]%
  Validation Guides: docs/validation/epic[EPIC_ID]_*.md
  Handoff: docs/handoff/epic[EPIC_ID]_handoff.md

  Technical Debt: [list or none]
  Ready for next epic

  Begin with Story [FIRST_STORY_ID].

  ---

  ## Recovery Prompt:

  Resume Epic [EPIC_ID] from handoff

  ---
