# WCC-NNNN: Specific symptom or mechanism

| Field | Value |
| --- | --- |
| Area | Owning component or failure layer |
| Status | Choose a defined status from CONTRIBUTING |
| Confidence | observed or confirmed, within the limits stated below |
| Evidence | runtime, source, runtime_and_source, or source_and_synthetic |
| Reported / reviewed | Date |
| Affected versions | Exact versions, or not established |
| Confirmed fixed versions | Exact versions and evidence link, or none established |
| Tracking issue | Link after the issue exists |

## Symptoms

What the person observes and the expected behavior. Avoid assigning a cause here unless it is already established.

## Evidence

A bounded, sanitized observation or reproducible synthetic case. Identify version, platform, observation window, and what the evidence cannot establish. Link public tests or upstream issues when available.

## Confirmed mechanism and hypotheses

State established facts separately from plausible explanations and unrelated failures. Describe how competing explanations could be distinguished.

## Containment or fix

Describe completed actions separately from proposed ones. Identify the owning component and exact scope. Do not embed raw private configuration or broad cleanup commands.

## Validation

Record the acceptance check, exact version/commit, date, result, and limitations. Passing a synthetic test does not establish a live product fix.

## Rollback

Explain the scoped reversal and any data/state limitations. If no change was made, say so.

## Unresolved work and same-issue reports

List the evidence needed next and what another affected person should report. Link related cases without merging distinct failure layers.

## References

Link authoritative protocol/product documentation, public regressions, relevant code commits, and upstream issue references. Never link a private raw diagnostic file.
