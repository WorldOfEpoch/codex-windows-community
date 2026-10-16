# WCC-0010: Compaction silently changes provider or model

| Field | Value |
| --- | --- |
| Area | conversation state |
| Status | `risk_documented` |
| Confidence | `confirmed` |
| Evidence | `source` |
| Reported / reviewed | October 16, 2026 |
| Affected versions | Not established; exact app build was not captured in the public record |
| Confirmed fixed versions | None established |
| Tracking issue | [Discussion and reports](https://github.com/WorldOfEpoch/codex-windows-community/issues/10) |

## Symptoms

The retired adapter could send a compaction request to a different provider/model from ordinary turns.

## Evidence

Source review found an explicit branch that redirected compaction from the experimental route to another provider/model and then returned subsequent ordinary requests to the original route. The current investigation did not establish that this branch caused the recent decoding or authorization failures.

This is a sanitized owner case study. The private source and incident evidence are not distributed. The [case index](README.md) defines the shared sample window and evidence limits.

## Confirmed mechanism and hypotheses

**Confirmed source behavior:** operation type could change the request destination and model without a separately expressed user choice.

**Unproven impact:** provider-specific state incompatibility, loss of context, or a particular failed recent session. A familiar API shape does not establish interchangeable compaction semantics.

## Containment or fix

The operational adapter is retired. The general provider lab requires explicit capability declarations; unsupported operations must fail clearly instead of silently switching destinations. A future compaction feature needs a documented provider-specific state contract.

## Validation

Source review establishes the behavior. No live cross-provider compaction test or repair was performed for this case. Any future support must be reported separately as authored, contract-tested, and live-validated for named versions.

## Rollback

Disable an experimental compaction path within its isolated adapter configuration. Do not rewrite or replace saved conversation state as an automatic fallback, and do not restore the retired provider.

## Unresolved work and same-issue reports

Contributors can define supported compaction inputs/outputs, continuity guarantees, and a synthetic failure case. If a provider legitimately delegates the operation, document that policy explicitly and validate that data handling and continuation remain correct.

Use this case ID when commenting on its tracking issue. Add your tested app/connector/adapter versions and what you observed; an additional report is not automatically an independent root-cause confirmation. For a different failure, open a new issue using the [report form](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml).

## References

- [Provider lab capability findings](https://github.com/WorldOfEpoch/codex-provider-compatibility-lab/blob/main/docs/compatibility-findings.md)
- [Tool-history case](WCC-0003-tool-history-validation.md)
