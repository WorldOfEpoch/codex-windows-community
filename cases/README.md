# Case index

Each record tracks one problem or source-proven risk. Its status is an evidence claim, not a judgment about all users or current product releases. [Contribution rules](../CONTRIBUTING.md) define the status fields.

| ID | Problem | Status | Evidence |
| --- | --- | --- | --- |
| [WCC-0001](./WCC-0001-global-relay-refusal.md) | Global relay dependency and connection refusal | `contained_locally` | `runtime_and_source` |
| [WCC-0002](./WCC-0002-watcher-restarts-and-stale-pids.md) | A restart watcher outlives relay removal | `contained_locally` | `runtime_and_source` |
| [WCC-0003](./WCC-0003-tool-history-validation.md) | Tool-history validation must follow each item type | `regression_documented` | `source_and_synthetic` |
| [WCC-0004](./WCC-0004-blender-helper-trees.md) | Repeated Blender connector helper trees | `contained_locally` | `runtime` |
| [WCC-0005](./WCC-0005-stream-framing-and-body-limits.md) | Relay stream framing and response-body limits | `risk_documented` | `source` |
| [WCC-0006](./WCC-0006-thread-read-access-denied.md) | Repeated thread/read access-denied failures | `unresolved` | `runtime` |
| [WCC-0007](./WCC-0007-notification-reconnects.md) | Cloud notification reconnect schedules | `unresolved` | `runtime` |
| [WCC-0008](./WCC-0008-app-server-websocket-1006.md) | App-server WebSocket closes with code 1006 | `unresolved` | `runtime` |
| [WCC-0009](./WCC-0009-optional-connector-discovery.md) | Repeated discovery failures from an optional connector | `contained_locally` | `runtime` |
| [WCC-0010](./WCC-0010-silent-compaction-provider-switch.md) | Compaction silently changes provider or model | `risk_documented` | `source` |
| [WCC-0011](./WCC-0011-unrelated-credential-startup-dependency.md) | Unrelated provider credentials block relay startup | `risk_documented` | `source` |

Use the stable case ID in issues and pull requests. A case's tracking issue holds discussion and new test results; the case file is the maintained summary. The [JSON index](index.json) provides the same IDs, paths, and review state for future tooling. It does not run anything.

## Scope of the initial evidence

The initial owner investigation examined a bounded October 16, 2026 log sample and selected retired integration source. The log window was 00:00:00–13:15:05 UTC. A routing change at 11:09:34 UTC defines the comparison boundary. The final scoped process check was at 13:22:35 UTC. A short earlier quiet sample did not establish durable resolution.

Counts describe records in that sample. Repeated UI state changes, retries, and scheduling records can refer to the same underlying failure. Before/after windows have different lengths. Several changes were made during cleanup and already-open clients could retain old settings; this was not a controlled attribution experiment.

Private logs, account data, local paths, process IDs, connector endpoints, and original private integration files are not published. These records preserve verified conclusions and limitations, not a complete diagnostic bundle. The source-only cases describe that retired custom implementation, not an asserted defect in every Codex or provider release.

No confirmed fixed Codex version is claimed in the initial records. The old Space Bunny integration remains retired and is not required to reproduce synthetic cases in the [provider compatibility lab](https://github.com/WorldOfEpoch/codex-provider-compatibility-lab).

Start a new record from [TEMPLATE.md](TEMPLATE.md). For a matching symptom, contribute to the existing issue or use the [problem-report form](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml).
