# WCC-0002: A restart watcher outlives relay removal

| Field | Value |
| --- | --- |
| Area | process lifecycle |
| Status | `contained_locally` |
| Confidence | `confirmed` |
| Evidence | `runtime_and_source` |
| Reported / reviewed | October 16, 2026 |
| Affected versions | Not established; exact app build was not captured in the public record |
| Confirmed fixed versions | None established |
| Tracking issue | Pending publication; link the issue carrying this case ID |

## Symptoms

Stopping a relay alone did not remove the background watcher that could start it again.

## Evidence

Source review found a watcher that invoked the router starter every ten seconds. During cleanup, its saved process receipt did not identify the actual running watcher. The old starter already used a startup mutex, so this is not evidence that it always created duplicate relays.

This is a sanitized owner case study. The private source and incident evidence are not distributed. The [case index](README.md) defines the shared sample window and evidence limits.

## Confirmed mechanism and hypotheses

**Confirmed:** the watcher was a separate process with a repeated startup loop; stopping only the relay left a mechanism that could bring it back. Trusting a stale process ID was insufficient for finding the current watcher.

**Not established:** that every observed process restart or duplicate helper was caused by this watcher. It did not contain Blender launch logic.

## Containment or fix

The existing removal owner was corrected to remove the sign-in entry, find the watcher using its verified executable and exact script identity, and stop the watcher even when retaining the relay for active clients. Removal was made safe to repeat after the routing block was already absent.

## Validation

The watcher and sign-in entry were absent in subsequent checks, including the final 13:22:35 UTC check on October 16. Configuration content was unchanged during the watcher-only follow-up. One relay was intentionally retained for open clients. This verifies local containment, not a general-purpose Windows process remover.

## Rollback

Keep removal narrow. Do not stop a process solely because a saved PID matches or because its executable name is common. If a different, supported service is deliberately restored later, restore its own documented startup mechanism and verify its identity. Do not restore the retired integration.

## Unresolved work and same-issue reports

A reusable lifecycle implementation needs tests for stale receipts, process-ID reuse, repeated removal, concurrent starts, readiness failure, and retention of an intentionally active relay. The provider lab's foreground client avoids this background lifecycle entirely.

Use this case ID when commenting on its tracking issue. Add your tested app/connector/adapter versions and what you observed; an additional report is not automatically an independent root-cause confirmation. For a different failure, open a new issue using the [report form](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml).

## References

- [Related routing case](WCC-0001-global-relay-refusal.md)
- [Provider compatibility lab](https://github.com/WorldOfEpoch/codex-provider-compatibility-lab)
