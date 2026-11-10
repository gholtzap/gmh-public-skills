# Guidance by work type

Read only the sections that affect the task. The examples explain ownership decisions; they do not require these components in every system.

## APIs, services, and SDKs

Design an operation around a consumer outcome. Put authoritative validation, access control, and transactional rules on the trusted side of the boundary. Avoid forcing each client to repeat dependent reads or reconstruct a server workflow. Separate safe reads from commands that can create side effects, including during automatic refresh or replay.

Use the existing contract format and derivation tools. An operation added to the source contract should reach the affected client without a second handwritten catalog. If generation is not available or justified, use explicit mappings and contract checks that prevent drift. Do not introduce a new RPC framework to make a small feature fit this pattern.

A public client must support the promised operation and relevant lifecycle without private app imports or copied presentation logic. Add client helpers only for a concrete local need, such as stream assembly, connection recovery, or protocol interpretation. Do not build another client solely to demonstrate hypothetical portability. When portability is requested, test a public consumer in the claimed environment.

Example: a rename action should call the existing authorized rename operation. It should not import database code into the UI or repeat access rules there. On failure, preserve edits; on success, reconcile the affected views through the existing data owner.

## Libraries, packages, and CLIs

Treat the public import or command as the contract. Include relevant argument validation, errors or exit codes, output format, side effects, and compatibility. Keep machine-readable output stable when consumers depend on it. Do not add a network API to an in-process library or local command without a consumer need.

For distributable packages, check the built or packed artifact through public entry points in an isolated consumer when exports, dependencies, or runtime support change. Workspace aliases can hide missing files and dependencies. Keep optional host integrations separate when the base package promises to work without them.

For a CLI change, invoke the actual command against representative input and inspect its output and side effects. For example, a parser fix needs to reach the installed entry point; importing its internal function cannot establish that the command uses it.

## Frontend and native applications

Use the existing design system, platform conventions, and asynchronous data primitives. Keep reusable product policy below presentation. Host synchronization, such as focus, navigation, or a device subscription, belongs near the host that owns it. Framework effects can be suitable there; they should not become a second owner for derived state or request policy.

Reuse the existing client and cache at their intended scope. Do not create a new cache per feature by default. Separate state owners when they need independent update rates or lifetimes; avoid wrappers that only pass values through. Keep local drafts separate from authoritative records and define how updates affect them.

Check the changed action and relevant loading, empty, error, and recovery states. Preserve draft, focus, scroll, and useful content where required. Inspect rendered behavior, accessibility, and layout at the applicable sizes and themes. Run the repository's required UI policy checks. A screenshot or layout pass alone does not prove the action works.

Use installed framework versions and official integration patterns. Do not require an upgrade, compiler, query library, or cross-platform component model solely because this skill is active.

## Systems code, protocols, and concurrent work

Let the protocol specification and language's ownership model guide the boundary. Keep wire parsing separate from trusted internal state, and reject malformed input before it can corrupt that state. Preserve framing, byte order, version negotiation, and failure containment when they are part of the changed contract.

Make ownership of buffers, locks, tasks, and queues explicit. A change to sharing or allocation must preserve lifetimes and synchronization. Check relevant bounds, backpressure, shutdown, and failure cleanup. Avoid introducing abstraction costs into a hot path without a concrete benefit and measurement.

Example: reusing a packet buffer can reduce allocation, but the result is invalid if a concurrent consumer can observe overwritten bytes. Validate delivery and ownership as well as allocation counts.

## Infrastructure, CI, and operational automation

Treat configuration, plans, commands, and exit results as consumer contracts. Reuse the existing deployment and workflow primitives. Keep environment-specific values at their owner, and separate a reusable operation from the host's credentials and permissions.

Check repeat execution, partial failure, concurrency, and recovery where relevant. Use plans, dry runs, or disposable environments for the evidence they can supply. A valid configuration does not prove a rollout; a local execution does not prove hosted CI or production acceptance.

Do not remove validation, security controls, required jobs, or supported platforms to claim an improvement. Execute external changes only within the user's authorization. Preserve required data and recovery paths; name any remaining execution gate.

## Performance and resource changes

Choose a user-relevant metric and record a baseline before changing the implementation. Compare equivalent inputs, success criteria, resource limits, runtime settings, and cache conditions. Repeat measurements enough to distinguish an effect from noise.

Check material tradeoffs: latency distributions, throughput, memory, startup, cost, correctness, and recovery as applicable. A speed gain that drops work or changes the workload does not establish the claimed improvement. Keep local benchmark claims separate from deployment-wide claims.

Prefer fixing repeated work, unnecessary data movement, or a poor primitive before adding caches or concurrency. If caching is justified, specify its key, identity scope, bounds, invalidation, and stale-data behavior.
