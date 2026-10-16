# WCC-0001: Global relay dependency and connection refusal

| Field | Value |
| --- | --- |
| Area | model routing |
| Status | `contained_locally` |
| Confidence | `confirmed` |
| Evidence | `runtime_and_source` |
| Reported / reviewed | October 16, 2026 |
| Affected versions | Not established; exact app build was not captured in the public record |
| Confirmed fixed versions | None established |
| Tracking issue | Pending publication; link the issue carrying this case ID |

## Symptoms

An experimental model route also carried ordinary model traffic, so an unavailable local relay caused ordinary requests to fail.

## Evidence

The owner's October 16, 2026 investigation found 37 backend WebSocket refusal records targeting the old local relay before routing removal and one afterward. Twenty-nine response-retry records and six startup/prewarm records also mentioned refusal before removal; these categories overlap and are not unique outage counts.

Source review confirmed that the installer changed the built-in provider's global base URL and forwarded non-experimental models through the same process. Six HTTP 426 records also matched its deliberate WebSocket rejection. The sampled Codex release version was not captured in the public evidence; affected-version boundaries are unknown.

This is a sanitized owner case study. The private source and incident evidence are not distributed. The [case index](README.md) defines the shared sample window and evidence limits.

## Confirmed mechanism and hypotheses

**Confirmed:** ordinary model requests depended on the experimental relay. Removing a configuration entry did not instantly change settings already loaded by open clients.

**Not established:** that this relay caused thread authorization failures, cloud notification failures, every reconnect, or any Blender process launch.

## Containment or fix

The owner removed the global route and custom catalog override, removed the sign-in startup entry, and retained one existing relay temporarily for open sessions. The old experimental provider remains retired. New experiments should use explicitly selected provider profiles and an isolated client configuration.

## Validation

Configuration checks confirmed the two overrides were absent. A later refusal still targeted the old relay after the edit, so this is containment with a remaining cached-client boundary, not a completed direct-routing acceptance test. A full clean-client comparison was not performed.

## Rollback

Preserve a private configuration backup before a scoped change. Restore only settings intentionally changed, after checking for newer edits. This incident is not a recommendation to restore the retired provider or to replace an entire configuration file.

## Unresolved work and same-issue reports

A clean new client session must be shown to use its intended provider without the retired listener. Contributors should record app version, provider selection method, whether a global override exists, and the endpoint class (direct, local relay, or remote gateway), without posting the endpoint itself.

Use this case ID when commenting on its tracking issue. Add your tested app/connector/adapter versions and what you observed; an additional report is not automatically an independent root-cause confirmation. For a different failure, open a new issue using the [report form](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml).

## References

- [Provider lab: explicit selection and lifecycle](https://github.com/WorldOfEpoch/codex-provider-compatibility-lab/blob/main/docs/compatibility-findings.md)
- [OpenAI advanced configuration](https://learn.chatgpt.com/docs/config-file/config-advanced)
