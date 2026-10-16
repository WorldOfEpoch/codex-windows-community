# WCC-0011: Unrelated provider credentials block relay startup

| Field | Value |
| --- | --- |
| Area | provider isolation |
| Status | `risk_documented` |
| Confidence | `confirmed` |
| Evidence | `source` |
| Reported / reviewed | October 16, 2026 |
| Affected versions | Not established; exact app build was not captured in the public record |
| Confirmed fixed versions | None established |
| Tracking issue | [Discussion and reports](https://github.com/WorldOfEpoch/codex-windows-community/issues/11) |

## Symptoms

A relay serving ordinary model traffic required another provider's key before it could listen.

## Evidence

The retired router's initialization read and validated the experimental provider's saved key unconditionally, before starting its listener. The same listener also carried ordinary requests for a different provider.

No key value was inspected or published. The recent failures do not prove that the key loader failed; this is a source-confirmed failure path.

This is a sanitized owner case study. The private source and incident evidence are not distributed. The [case index](README.md) defines the shared sample window and evidence limits.

## Confirmed mechanism and hypotheses

**Confirmed source risk:** one provider's missing or unreadable credential could prevent an unrelated provider's route from starting.

**Unproven incident attribution:** this failure path caused any of the observed refusal records. Listener unavailability has several possible causes.

## Containment or fix

The global relay dependency was removed. New general adapters should acquire only the credential selected for the current explicit provider profile and should not require unrelated providers to be configured.

## Validation

Source review established the ordering and dependency. No credential was deleted, rotated, exposed, or intentionally broken to reproduce this case. There is no live failure/recovery claim.

## Rollback

A provider-isolation fix should be reversible in the adapter code or isolated profile. Never test rollback by sharing credentials between accounts or restoring private credential files from a public artifact.

## Unresolved work and same-issue reports

Add a synthetic test where an unused provider has no credential and the selected provider remains usable, plus a content-free error test when the selected provider's credential is missing. Real secrets are unnecessary.

Use this case ID when commenting on its tracking issue. Add your tested app/connector/adapter versions and what you observed; an additional report is not automatically an independent root-cause confirmation. For a different failure, open a new issue using the [report form](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml).

## References

- [Global relay dependency](WCC-0001-global-relay-refusal.md)
- [Provider lab](https://github.com/WorldOfEpoch/codex-provider-compatibility-lab)
