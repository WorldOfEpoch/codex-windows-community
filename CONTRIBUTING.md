# Contributing

You can help by reporting a reproducible problem, confirming the same symptom on another version, testing a proposed fix, improving instructions, or contributing a synthetic regression case. A careful report that leaves the cause unknown is better than an unsupported diagnosis.

## Report the same issue

Search the [case index](cases/README.md) and repository issues before opening a new report. If the symptom and failure layer match, comment on the existing tracking issue with the case ID and the information below. If the layer differs or you are unsure, use the report form and link the possibly related case; maintainers can connect or split reports.

Provide:

- Codex app version and installation channel, Windows version, and relevant connector or adapter version. Write “unknown” when you cannot establish a value.
- The visible symptom, expected behavior, frequency, and a bounded observation period with timezone.
- Minimal reproduction steps using a new synthetic project or conversation when possible.
- A content-free error family or fixed diagnostic code, plus counts if useful.
- Provider setup class: direct, local relay, remote gateway, or unknown. Do not include endpoint URLs or credentials.
- What you changed, what happened, and whether you repeated the check or restarted the relevant client.
- Whether the result is a source-review inference, synthetic reproduction, or observed runtime behavior.

A “same issue” report confirms only the matching observations you provide. It does not automatically confirm the original proposed cause. Avoid posting repeated “me too” comments without version or impact information; a reaction can register interest.

## Propose a fix

Use the fix contribution form or a pull request. Include the owning component, the exact proposed change, a failing case before the change, the result afterward, relevant versions or commit IDs, known limitations, and a scoped rollback.

Prefer a minimal synthetic regression. Keep adapter code and executable transport tests in the [provider compatibility lab](https://github.com/WorldOfEpoch/codex-provider-compatibility-lab); link the relevant commit or pull request here instead of copying a second implementation. Changes to Codex itself belong with its upstream owner, with a reference recorded here when available.

Do not bundle automatic cleanup, unattended monitors, sign-in startup entries, new services, or broad process-killing commands into an issue fix. A new operational tool needs its own explicit design, scope, permissions, and tests. The current repository is documentation only.

## Evidence and status

These fields describe different things and must remain separate:

| Field | Value | Meaning |
| --- | --- | --- |
| Confidence | `observed` | The symptom occurred; its cause may still be unknown |
| Confidence | `confirmed` | The stated mechanism or source behavior is established within the case's explicit limits |
| Evidence | `runtime` | Observed running behavior or measured state |
| Evidence | `source` | Code/configuration review; not necessarily a reproduced incident |
| Evidence | `runtime_and_source` | Both are available and the case states how they relate |
| Evidence | `source_and_synthetic` | Source review plus an invented test case; no live-model claim |
| Status | `unresolved` | No verified remedy for the observed problem |
| Status | `risk_documented` | A source-proven risk with incident impact or repair still unverified |
| Status | `regression_documented` | A synthetic regression exists; live integration is a separate claim |
| Status | `contained_locally` | A scoped change reduced the local exposure or removed a dependency; no general fixed-version claim |
| Status | `fix_verified` | A reproducible fix has passed the stated acceptance check on explicitly listed versions |

For `fix_verified`, name exactly what was fixed, list the tested version or commit, link public regression evidence, retain limitations, and populate `confirmed_fixed_versions` in the JSON index. A local workaround, quiet ten-minute sample, passing build, closed issue, or edited setting is not enough by itself.

A version entry should identify its component, version/commit, platform, test date, acceptance check, and evidence link. Do not mark a Codex release fixed because an independent adapter test passed.

## Edit the case collection

Use [the case template](cases/TEMPLATE.md) for a new record. Assign the next unused stable ID after checking the current branch. Keep one problem per case, link related cases, and preserve unresolved alternatives rather than overwriting them with a new guess.

Update the case file, [human index](cases/README.md), and [JSON index](cases/index.json) in the same pull request. Keep IDs and paths stable. Add the tracking-issue link after it exists. When correcting a conclusion, explain which new evidence changes it and keep useful prior validation boundaries.

Every case must state symptoms, evidence, confirmed mechanism versus hypothesis, containment/fix, validation, rollback, and unresolved work. Include affected and tested versions; “not established” is an honest initial value. Describe completed actions separately from suggestions.

## Keep evidence safe and useful

Do not attach raw sessions, application databases, full logs, configuration files, process command lines, credentials, cookies, authorization headers, local usernames or file paths, endpoint URLs, process IDs, private project names, or screenshots containing them. These may reveal more than the error itself.

Summarize the error family and timing, or construct an invented fixture that reproduces the behavior. Preserve the original privately if it is needed for an authorized upstream investigation. Review every proposed attachment yourself; replacing one token does not guarantee a diagnostic bundle is safe.

Security-sensitive findings follow [SECURITY](SECURITY.md). Contributors retain ownership of their contributions and submit them under this repository's MIT license. Include only material you have permission to share.
