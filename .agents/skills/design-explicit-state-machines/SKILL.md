---
name: design-explicit-state-machines
description: Design, change, or review software workflows with explicit states and enforced transition rules. Use for lifecycle logic, status flags, asynchronous operations, retries, and cancellation. Prefer explicit models and allow implicit workflows only when clearly necessary.
---

# Design explicit state machines

Use explicit state machines for workflows in the requested scope. An atomic operation with no lifecycle does not need a state machine. An explicit model names the states, events, and rules that permit transitions. An enum alone is not enough.

Use an implicit workflow only when an explicit model cannot meet a concrete requirement. Convenience, less code, or an existing flag pattern is not sufficient reason to choose an implicit workflow.

## Read the existing workflow

Trace the callers, state writers, storage, and external effects before changing code. Reuse or strengthen existing transition helpers and domain operations. Preserve supported behavior. Do not migrate unrelated workflows or add a state machine library by default.

Before implementation, describe the current state, event, and rule in plain language. Keep one small transition table with the current state, event, required conditions, next state, and effects. Include repeated requests and invalid events. Separate existing behavior from proposed behavior, and update the table as the design changes.

## Choose the correct state boundaries

| Design concern | Required approach |
|---|---|
| Independent facts | Use separate state dimensions or cooperating machines. A document can be Published and Locked. Define any rules between them. |
| Calculated conditions | Store authoritative facts and derive a named state through one shared function. An invitation can derive Expired from expiresAt and the current time. Do not add a second stored status that can become stale. |
| Valid overlapping work | Track each operation and its data version separately. An editor can save version 4 while the user edits version 5. |
| Retries and delayed responses | Give attempts an identity. Check that a result belongs to the current permitted attempt before applying it. Define whether a repeated request returns the existing result, retries, or is rejected. |
| State-specific data | Keep required data with its state. Prefer types or validation that prevent impossible combinations, such as Success without its result. |

A state may be stored or calculated. A named state function over timestamps or other facts is explicit when its states and transition rules are defined. Do not duplicate stored data merely to add a status field.

## Enforce the rules

- Put each workflow's transitions behind a shared operation. UI, API, workers, and agents must use the same authoritative rules. UI button state is not enforcement.
- Prevent unrestricted state assignment outside that boundary. Validate loaded data and external events at the boundary.
- Where writers can overlap, use a transaction, version check, conditional update, or equivalent mechanism. Check the state and apply the update atomically.
- Define failure, cancellation, timeout, restart, and recovery where they apply. Decide what happens to late results and external effects that finish after cancellation.
- Treat external effects separately from local state updates. Use request keys and recovery checks where needed. A state machine alone does not guarantee one-time email delivery, payment, or cloud-resource creation.

## Verify the behavior

List the relevant failure cases before implementation. Verify valid transitions, rejected transitions, repeated requests, stale results, concurrent updates, and recovery where applicable. Check that independent facts and valid overlapping work still function. Retain repeatable evidence appropriate to the task.

## Permit an implicit workflow only by exception

First try a small explicit transition function, calculated state, or separate cooperating machines. If none can satisfy a concrete requirement, state that requirement, explain why the explicit options fail, and identify the remaining implicit state and its safeguards. Keep the exception narrow. Do not invent a requirement to justify an exception.

Explain the delivered behavior with one concrete example. Link to the transition table when it is already in a reviewable artifact; otherwise include the table in the response. Keep implementation details after the behavior. State any exception or unverified behavior briefly; do not present a design review as a confirmed runtime result.
