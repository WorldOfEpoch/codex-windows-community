# WCC-0008: App-server WebSocket closes with code 1006

| Field | Value |
| --- | --- |
| Area | app-server transport |
| Status | `unresolved` |
| Confidence | `observed` |
| Evidence | `runtime` |
| Reported / reviewed | October 16, 2026 |
| Affected versions | Not established; exact app build was not captured in the public record |
| Confirmed fixed versions | None established |
| Tracking issue | Pending publication; link the issue carrying this case ID |

## Symptoms

App-server transport closure records reported code 1006; repeated UI status lines overstated the apparent incident count.

## Evidence

The bounded October 16 sample contained eight transport-closed records with code 1006 before route removal and one afterward. These nine records used WebSocket transport and were not marked as app-quitting events. Many additional state-change lines repeated the closure information; they were excluded from this count.

This is a sanitized owner case study. The private source and incident evidence are not distributed. The [case index](README.md) defines the shared sample window and evidence limits.

## Confirmed mechanism and hypotheses

**Observed:** abnormal WebSocket closures were reported, followed by state updates and recovery activity.

**Unknown:** the initiating failure. The error code alone does not identify an authentication, server, network, model, or plugin root cause. No causal chain from the retired relay was established.

## Containment or fix

No remote service was restarted, no security setting was weakened, and no provider was re-enabled. Correlate one transport-close record with nearby safe event types before treating repeated UI lines as independent failures.

## Validation

A transport-close record persisted after local routing removal. No fixed version or successful targeted repair was established. The nine records are not guaranteed to represent nine distinct user-visible outages.

## Rollback

No specific change was applied. Future fixes must document the owning component and a scoped reversal path rather than resetting unrelated settings.

## Unresolved work and same-issue reports

Needed: exact app version, connection type in general terms, bounded timing, observable interruption, and a reproducible failure or upstream diagnosis. Link a same-issue report only when symptoms and transport layer match.

Use this case ID when commenting on its tracking issue. Add your tested app/connector/adapter versions and what you observed; an additional report is not automatically an independent root-cause confirmation. For a different failure, open a new issue using the [report form](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml).

## References

- [Notification reconnect case](WCC-0007-notification-reconnects.md)
- [Safe evidence requirements](../CONTRIBUTING.md)
