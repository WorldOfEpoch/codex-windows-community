# WCC-0007: Cloud notification reconnect schedules

| Field | Value |
| --- | --- |
| Area | notification transport |
| Status | `unresolved` |
| Confidence | `observed` |
| Evidence | `runtime` |
| Reported / reviewed | October 16, 2026 |
| Affected versions | Not established; exact app build was not captured in the public record |
| Confirmed fixed versions | None established |
| Tracking issue | [Discussion and reports](https://github.com/WorldOfEpoch/codex-windows-community/issues/7) |

## Symptoms

The desktop notification transport repeatedly scheduled reconnects, including after local routing removal.

## Evidence

The October 16 bounded sample contained 123 notification reconnect-schedule records before local route removal and 15 afterward. A schedule record is an attempted recovery event, not proof of a distinct outage, failed model response, or user-visible interruption.

This is a sanitized owner case study. The private source and incident evidence are not distributed. The [case index](README.md) defines the shared sample window and evidence limits.

## Confirmed mechanism and hypotheses

**Observed:** reconnect scheduling continued across the configuration change.

**Unknown:** whether the cause was remote service behavior, network interruption, authentication/state changes, client lifecycle, or a combination. The inspected local model router did not implement the notification transport.

## Containment or fix

No network-priority change, firewall relaxation, account reset, or background monitor was installed. Keep this investigation separate from model endpoint failures so a routing change is not credited with fixing unrelated transports.

## Validation

Notifications continued to schedule reconnects after the route change. This establishes persistence in the sampled period, not long-term frequency or a diagnosed root cause. No fix is confirmed.

## Rollback

No specific change was applied for this case. If testing a future networking or client change, record exactly one change and its reversal path; do not alter security controls just to make a counter decrease.

## Unresolved work and same-issue reports

Contributors should distinguish scheduled reconnects from lost notifications, record app version and a bounded time window, and describe observable impact. Record network transitions in general terms without publishing addresses or device identifiers.

Use this case ID when commenting on its tracking issue. Add your tested app/connector/adapter versions and what you observed; an additional report is not automatically an independent root-cause confirmation. For a different failure, open a new issue using the [report form](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml).

## References

- [App-server WebSocket closures are tracked separately](WCC-0008-app-server-websocket-1006.md)
- [Global relay refusal case](WCC-0001-global-relay-refusal.md)
