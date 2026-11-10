---
name: make-state-machines-explicit
description: Find implicit application workflows, convert them with user consent, and audit the result for unnecessary or duplicate states. Use for app-wide state-machine discovery and refactoring.
---

# Make state machines explicit

## 1. Inventory without edits

Enumerate UI actions, API/SDK commands, workers, callbacks, and recovery paths. Trace callers, guards, runtime contracts, persistence, and external effects. Look for workflows encoded in flags, nulls, timestamps, record existence, scattered conditionals, or repeated status writes.

Report each workflow's actions, states, transitions, owner, source locations, and classification: explicit, partial, implicit, or atomic/no lifecycle needed. Explicit means named states, events, and enforced rules; an enum alone is insufficient. Shared calculated states can be explicit. Cross-check against the entrypoints and disclose coverage gaps before claiming completeness.

## 2. Convert after consent

Present the proposed scope, migration, and transition table: current state → event → conditions → next state → effects. Include retries and invalid actions. Obtain user consent before application code or data changes. Earlier explicit authorization for that scope counts; invoking this skill alone does not authorize conversion.

After consent:

- Use existing primitives and the smallest explicit model. Keep independent facts separate and derive summaries from authoritative facts.
- Enforce transitions at the domain owner across UI, API, and workers. Validate external inputs and state-specific data.
- Preserve behavior and history. Use transactions, version checks, and fixed request identities where needed. Check that each result belongs to the current permitted attempt before applying it. Define applicable failure, cancellation, timeout, late-result, and restart behavior. An unknown external outcome does not permit an unsafe retry.
- Verify affected entrypoints, rejected transitions, replay, concurrency, and recovery. Run repository-required checks.

## 3. Audit and simplify

Recheck readers, writers, stored data, and tests. For every state, identify the distinct fact, permitted action, or recovery rule that requires it.

- Remove unreachable or constant states when no supported contract or historical data needs them.
- Derive duplicate summaries. An intermediate state that exists only within a transaction may still support validation or action history. Remove its stored representation only when no reader, rule, recovery path, or history requirement needs it.
- Merge only states with equivalent meaning and behavior. Preserve independent workflows and distinctions such as unknown versus confirmed failure, or delivery versus acceptance, settlement, and posting.

Simplify within the approved scope and rerun affected checks. Migrate data before removing representations; stop on ambiguous history instead of guessing. Report changes, justified remaining states, implicit workflows, verification, and coverage gaps. Distinguish source review from runtime proof.
