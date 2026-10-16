# WCC-0003: Tool-history validation must follow each item type

| Field | Value |
| --- | --- |
| Area | protocol validation |
| Status | `regression_documented` |
| Confidence | `confirmed` |
| Evidence | `source_and_synthetic` |
| Reported / reviewed | October 16, 2026 |
| Affected versions | Not established; exact app build was not captured in the public record |
| Confirmed fixed versions | None established |
| Tracking issue | Pending publication; link the issue carrying this case ID |

## Symptoms

Calls and tool results have different required fields; a generic rule can reject valid results or miss missing call IDs.

## Evidence

Review of the retired adapter found an incomplete history census: it checked function-call arguments and IDs, but only checked the output field for function results. The public provider lab contains synthetic cases for required IDs, valid empty results, function JSON arguments, and custom-tool text input.

These are protocol and validation findings. The recent local incident does not establish that any particular saved conversation was corrupted, or that malformed history caused the other error families.

This is a sanitized owner case study. The private source and incident evidence are not distributed. The [case index](README.md) defines the shared sample window and evidence limits.

## Confirmed mechanism and hypotheses

**Confirmed:** a function call and a function result are different shapes. A function result needs its call ID and output; it does not need the function name. An empty output string is not a missing field. A validator that does not check result IDs can miss broken linkage.

**Unproven for the recent incident:** the origin of any malformed history, its persistence, or its contribution to reconnects.

## Containment or fix

The provider lab implements type-specific shape checks and synthetic regressions. It rejects unsupported transformations explicitly and does not invent IDs or rewrite saved conversations. Use its documented subset rather than treating its inspector as a complete provider schema validator.

## Validation

The original published lab included passing synthetic tests for these cases. Use the CI run attached to the exact lab commit you test; there is no assertion here that a particular live model or saved conversation passed. No historical conversation repair was performed.

## Rollback

Validation should be read-only. Do not bulk-edit conversation histories or generate replacement call IDs as a repair. A code change can be reverted at its owning adapter commit; retain a minimal synthetic failing case.

## Unresolved work and same-issue reports

Contributors can add call/result matching and provider-specific schema cases with explicit acceptance rules. Report whether the failure is in a synthetic validator, an outgoing request, an incoming response, or a resumed conversation. Keep real history private.

Use this case ID when commenting on its tracking issue. Add your tested app/connector/adapter versions and what you observed; an additional report is not automatically an independent root-cause confirmation. For a different failure, open a new issue using the [report form](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml).

## References

- [Provider lab history findings and limitations](https://github.com/WorldOfEpoch/codex-provider-compatibility-lab/blob/main/docs/compatibility-findings.md)
- [OpenAI function calling](https://developers.openai.com/api/docs/guides/function-calling)
