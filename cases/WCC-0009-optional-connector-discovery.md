# WCC-0009: Repeated discovery failures from an optional connector

| Field | Value |
| --- | --- |
| Area | optional connectors |
| Status | `contained_locally` |
| Confidence | `observed` |
| Evidence | `runtime` |
| Reported / reviewed | October 16, 2026 |
| Affected versions | Not established; exact app build was not captured in the public record |
| Confirmed fixed versions | None established |
| Tracking issue | Pending publication; link the issue carrying this case ID |

## Symptoms

An optional presence connector repeatedly failed discovery and added background error noise.

## Evidence

The desktop sample contained 820 failure records associated with the optional presence connector before it was disabled, and ten later records before the end of the bounded sample. Connector discovery failures are different from model-provider failures. The integration's private endpoint and project-specific setup are intentionally excluded.

This is a sanitized owner case study. The private source and incident evidence are not distributed. The [case index](README.md) defines the shared sample window and evidence limits.

## Confirmed mechanism and hypotheses

**Observed:** repeated failures from one configured optional connector, including later references from still-open clients.

**Unknown:** whether its service was unavailable, its authentication or configuration was wrong, or its client lifecycle was responsible. The evidence does not show that the model router caused this connector to fail.

## Containment or fix

The owner disabled the unused optional connector in configuration. Its definition was retained, and no unrelated server or project was shut down. Open clients could still retain prior connector configuration, so the edit alone was not a clean restart test.

## Validation

The connector's enabled flag was false at verification. A short quiet interval was followed by later failures, so the record is local containment rather than a proven service repair. No verified fixed connector release is identified.

## Rollback

For an intentionally restored integration, reconcile its existing definition and authentication through its supported owner. Do not restore an entire configuration backup or publish the endpoint. The retired model provider is unrelated to this rollback.

## Unresolved work and same-issue reports

A reusable fix needs an isolated connector reproduction, explicit service readiness and authentication checks, bounded retry behavior, and a clean client lifecycle test. A same-issue report should describe the connector type and failure stage without exposing service URLs.

Use this case ID when commenting on its tracking issue. Add your tested app/connector/adapter versions and what you observed; an additional report is not automatically an independent root-cause confirmation. For a different failure, open a new issue using the [report form](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml).

## References

- [Blender helper case](WCC-0004-blender-helper-trees.md)
- [Contributor evidence levels](../CONTRIBUTING.md)
