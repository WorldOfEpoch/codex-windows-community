# WCC-0006: Repeated thread/read access-denied failures

| Field | Value |
| --- | --- |
| Area | authorization and client state |
| Status | `unresolved` |
| Confidence | `observed` |
| Evidence | `runtime` |
| Reported / reviewed | October 16, 2026 |
| Affected versions | Not established; exact app build was not captured in the public record |
| Confirmed fixed versions | None established |
| Tracking issue | Pending publication; link the issue carrying this case ID |

## Symptoms

Background thread reads repeatedly failed authorization; removing the model relay did not establish resolution.

## Evidence

The bounded October 16 desktop sample contained 49,936 thread-read denial records before the route-removal boundary and 4,727 afterward. The exact method was thread/read. Counts are log records and may repeat the same underlying failure; they are not a count of inaccessible conversations or affected users.

A quiet short interval during cleanup was followed by renewed denials. The comparison windows have different lengths and cannot establish a rate improvement.

This is a sanitized owner case study. The private source and incident evidence are not distributed. The [case index](README.md) defines the shared sample window and evidence limits.

## Confirmed mechanism and hypotheses

**Observed:** repeated failed background reads and continued polling.

**Unknown:** why authorization and client state disagreed. The inspected model relay did not implement desktop thread-read authorization. Shared timing or resource pressure is not proof that it caused this failure.

## Containment or fix

No authorization reset, account removal, history deletion, or permission widening was performed. This record deliberately has no claimed fix. Preserve a private diagnostic snapshot and identify the affected client/account context through supported product diagnostics.

## Validation

The error resumed after the earlier quiet interval and remained present in the bounded sample. There is no verified fixed release or successful targeted reproduction/repair for this case.

## Rollback

No containment mutation was applied, so there is nothing to roll back. Avoid restoring old account files or copying authentication material between profiles as an experiment.

## Unresolved work and same-issue reports

Needed: a minimal non-sensitive reproduction, app version, local versus remote conversation scope, whether a clean supported sign-in/session changes the result, and an upstream issue reference if one exists. Do not post account identifiers or real conversation IDs.

Use this case ID when commenting on its tracking issue. Add your tested app/connector/adapter versions and what you observed; an additional report is not automatically an independent root-cause confirmation. For a different failure, open a new issue using the [report form](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml).

## References

- [Global model routing is a separate case](WCC-0001-global-relay-refusal.md)
- [How to report the same issue](../CONTRIBUTING.md)
