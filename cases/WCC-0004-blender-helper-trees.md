# WCC-0004: Repeated Blender connector helper trees

| Field | Value |
| --- | --- |
| Area | optional connectors |
| Status | `contained_locally` |
| Confidence | `observed` |
| Evidence | `runtime` |
| Reported / reviewed | October 16, 2026 |
| Affected versions | Not established; exact app build was not captured in the public record |
| Confirmed fixed versions | None established |
| Tracking issue | [Discussion and reports](https://github.com/WorldOfEpoch/codex-windows-community/issues/4) |

## Symptoms

Multiple verified Blender connector helpers were running; a connector status notification alone is not proof of a new process.

## Evidence

The cleanup verified and stopped 14 Blender connector launcher processes and their matching Python descendants. No Blender application was running in the initial inspection. The optional connector was disabled in the user's configuration.

Five later ready-status records appeared. Backend records around those times referred to cached catalogs or pending optional servers; the later stderr sample showed a tool-list request. They did not provide five new process-start receipts.

This is a sanitized owner case study. The private source and incident evidence are not distributed. The [case index](README.md) defines the shared sample window and evidence limits.

## Confirmed mechanism and hypotheses

**Observed:** multiple helper process trees existed, and open clients continued to reference connector state after the configuration edit.

**Not established:** the complete parentage of every historical launch, whether all helpers were unintended duplicates, or a causal link to the experimental model router. The inspected model router did not launch Blender.

## Containment or fix

The owner disabled this optional connector, verified the exact helper identities, and stopped those process trees. The Blender application and unrelated Python processes were not cleanup targets. This is a scoped containment example, not a command to terminate every process with a familiar name.

## Validation

The final October 16 check found zero matching launchers and zero matching Python children. Later ready notifications were evaluated against live process evidence rather than counted as new launches. Long-term recurrence after a full client restart remains unverified in this record.

## Rollback

Only restore a connector when its use is intended and its owner is known. Re-enabling a connector and starting an application are separate actions. Preserve configuration changes made after the backup and do not restore the retired model router.

## Unresolved work and same-issue reports

A useful reproduction must establish which client created each helper, whether processes survive client shutdown, and whether a new start time appears after containment. Share counts and elapsed times; keep process command lines, local paths, and raw process IDs private.

Use this case ID when commenting on its tracking issue. Add your tested app/connector/adapter versions and what you observed; an additional report is not automatically an independent root-cause confirmation. For a different failure, open a new issue using the [report form](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml).

## References

- [Watcher case: a different lifecycle](WCC-0002-watcher-restarts-and-stale-pids.md)
- [Safe reporting guidance](../CONTRIBUTING.md)
