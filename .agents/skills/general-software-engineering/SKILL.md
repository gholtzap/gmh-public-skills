---
name: general-software-engineering
description: Design, implement, refactor, and review software with clear consumer contracts, sound primitives, explicit ownership, and complete behavior checks. Use for engineering changes across applications, services, libraries, CLIs, systems code, and infrastructure, especially when deciding where behavior belongs. Adapt to the existing language, stack, and scope.
---

# General software engineering

## Fit the task

Apply this guidance to the requested behavior and affected callers. Follow the repository's contracts, tools, and conventions; use task-specific skills where needed. A review can end with findings and require no edits.

Read only the relevant sections of [guidance by work type](references/work-types.md). Add structure or infrastructure only when the requested work needs it.

## Inspect before you extend

Read the relevant implementation, callers, tests, and configuration before a change. Trace the current path from the entry point to its result and side effects. Look for existing operations, types, validation, state owners, error handling, and test helpers that can do the work.

Before adding behavior, decide:

- Does the behavior or a useful part of it already exist?
- Would this change copy a rule, contract, or state that has an owner?
- Is a hidden assumption causing callers to compensate for a weak primitive?
- Would a small change to that primitive remove duplication or make correctness easier to check?

Improve the existing owner first when it makes this task simpler or more correct. Otherwise keep the change local. Similar syntax alone does not prove that two behaviors need the same abstraction. Do not build extension points for imagined callers.

## Start with a consumer contract

Choose one observable outcome. Write or identify its intended use: a function call, command, request, event exchange, configuration, or user action. Use the language and level of detail appropriate to the task; a short note or test can be enough.

Define the relevant inputs, result, failures, side effects, and compatibility constraints. For work that crosses boundaries, include identity and authorization, resource ownership, and any retry or cancellation semantics that affect correctness. Identify which existing owners must change and which can stay as they are.

Make ordinary use simple without hiding material choices. The caller should not need private imports, copied business rules, undocumented ordering, or repeated transport details.

## Keep contracts and behavior at their owner

Define each domain rule, public contract, and authoritative fact once. Generate types, clients, serializers, and adapters from the contract where supported, using the existing tools. Derive calculated values instead of storing copies that need synchronization.

Validate untrusted data where it enters the system. Use the project's suitable runtime schemas, parsers, codecs, or language types. Static types alone do not validate external input. Do not add redundant runtime checks to every trusted internal call.

Keep distinct concepts distinct. A wire value, stored record, editable draft, and public result can have different shapes and lifetimes. Name and test necessary conversions; avoid duplicate definitions that can drift. External protocols remain authoritative where they define the contract. Preserve supported versions and consumers when changing a boundary.

- Domain code owns rules and legal operations. Persistence owns storage mechanics. Transport owns encoding and delivery. Presentation owns interaction and rendering. These are responsibilities, not required packages or files.
- Enforce authorization in trusted code. Disabled buttons and client checks cannot replace it. Put coordination where the required permissions, data, and workflow belong; account for offline, local, privacy, and latency needs.
- Keep reusable policy out of a specific UI or host adapter. Expose only the operation and local behavior that actual consumers need. Do not create a second business implementation in a client SDK.
- Use public entry points when calling another module or package. Keep privileges, secrets, and runtime-specific dependencies out of consumers that cannot use them. Use existing export and import conventions.
- Isolate a vendor dependency when its protocol, failure behavior, privileges, or replacement cost creates a useful boundary. An adapter should own behavior or narrow a contract. Wrapping every import adds no such value.

Use functions, modules, traits, classes, or services as the project needs. Add a separate interface only when it expresses a real contract that the existing type cannot supply.

## Pass dependencies and manage resources

Pass only the dependencies an operation needs. Let the code that selects an implementation supply it. Ordinary arguments often suffice; use the repository's dependency mechanism when present. Do not add containers or per-function factories merely to show dependency injection.

Define where connections, tasks, caches, files, and subscriptions are created, shared, and released. Share them only when their users can safely share identity, data, and updates. Keep tenant, credential, and request data isolated where required.

Split unrelated workflows into separate operations when mode flags obscure their behavior or allow invalid combinations. Keep configuration, type tags, and booleans when they express the behavior clearly. Do not replace a clear conditional with a framework.

## Make state and failure behavior explicit

Define when caches and drafts become stale and how they are reconciled with authoritative data.

When lifecycle complexity matters, name the legal states and transitions. Use the language's suitable enum, tagged union, transition function, or state model. Avoid independent flags that permit invalid combinations. Check exhaustiveness where supported, and still handle unknown external values at the boundary.

Distinguish states that require different behavior: for example, pending work, an empty result, cancellation, partial completion, and a recoverable failure. Keep useful data during refresh when the product requires it. Do not infer completion from an empty collection.

Return failures that callers can act on, preserve useful causes, and avoid exposing secrets. Never replace a failed operation with fake success. Retry only when repeating the operation is safe or the receiver reliably prevents duplicate effects. Bound retries and queues; define cleanup and partial results where cancellation or failure can interrupt side effects. Use transactions, version checks, or locks when concurrent work could break a required rule.

## Build and verify the requested path

Identify the smallest complete behavior that satisfies the request. Ask only when a missing decision changes the result. For a new capability, implement it at its owner, connect its real consumer, and exercise the outcome before expanding to more capabilities. For a repair, start at the owner of the fault and follow affected callers outward. Reuse unchanged layers.

Run the relevant existing checks and add tests where they catch a meaningful failure. Test behavior and contracts rather than file layout or internal call sequences. Use an integration or end-to-end check when the risk crosses boundaries; use focused tests for rules or failures that the full path cannot exercise well. Do not create redundant tests for a trivial reversible edit.

Exercise the actual entry point and verify the visible result or saved change, plus relevant failures and recovery. Use mocks to control external dependencies where needed. Types, lint, internal calls, mocks, and screenshots establish only what they check; they do not establish that an untested user flow works.

Run applicable architecture checks. Add a new check only for an important recurring rule within the task. Do not weaken a policy or remove a check to get a pass. Measure performance claims under comparable conditions and check material tradeoffs.

## Finish with evidence

State the resulting behavior, the important contract or ownership change, and the checks actually performed. Identify material compatibility limits and blocked or untested paths. Keep local checks, CI, merge, deployment, and live acceptance distinct when relevant. Limit claims to the evidence collected.

Keep the explanation proportional to the change. Use existing code, tests, and review artifacts; create separate planning or status documents only when requested or needed for the work.
