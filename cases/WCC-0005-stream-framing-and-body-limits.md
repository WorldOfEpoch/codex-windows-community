# WCC-0005: Relay stream framing and response-body limits

| Field | Value |
| --- | --- |
| Area | transport |
| Status | `risk_documented` |
| Confidence | `confirmed` |
| Evidence | `source` |
| Reported / reviewed | October 16, 2026 |
| Affected versions | Not established; exact app build was not captured in the public record |
| Confirmed fixed versions | None established |
| Tracking issue | Pending publication; link the issue carrying this case ID |

## Symptoms

The retired relay had stream and body-handling risks, but recent decoding failures cannot be assigned to a particular one.

## Evidence

Source review found that the experimental-route translator parsed each data line separately, passed JSON parse failures through, had no complete-event size bound, and flushed an unfinished trailing line. The error path captured only part of some upstream bodies while retaining upstream framing headers. Compressed requests were bounded before synchronous decompression, without a decoded-size bound.

Seven recent backend response-body decoding errors were observed between 10:37:49 and 10:58:54 UTC on October 16. This is correlation only: normal upstream success responses used a different branch, and no captured response proved which mechanism produced those errors.

This is a sanitized owner case study. The private source and incident evidence are not distributed. The [case index](README.md) defines the shared sample window and evidence limits.

## Confirmed mechanism and hypotheses

**Confirmed source risks:** stream chunks and individual lines are not necessarily complete events; truncated bodies can disagree with declared length or encoding; compressed size does not bound decoded size.

**Unproven runtime attribution:** that these risks caused the seven observed decoding errors, memory exhaustion, or all reconnects.

## Containment or fix

The operational relay is retired. The provider lab is the owner of reusable transport work and synthetic regressions. It must distinguish event assembly, total response size, decoded size, HTTP errors, cancellation, and completion rather than treating them as one generic reconnect.

## Validation

The initial public lab exercised event boundaries, split UTF-8, line endings, multi-line data, malformed JSON, and unfinished events. Current HTTP and limit coverage must be checked against the exact lab commit and CI run. No live reproduction of the private decoding failures is claimed.

## Rollback

Revert changes in an isolated adapter test environment, not in an active user's entire configuration. Preserve a failing synthetic fixture. Do not restart the retired relay to reproduce this case.

## Unresolved work and same-issue reports

Contributors should supply a local synthetic server or fixture that fails before a fix and passes afterward. Distinguish compressed input, decoded content, one event, and the whole response. Include tests that truncated or unfinished responses fail clearly without automatic model replay.

Use this case ID when commenting on its tracking issue. Add your tested app/connector/adapter versions and what you observed; an additional report is not automatically an independent root-cause confirmation. For a different failure, open a new issue using the [report form](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml).

## References

- [Provider lab streaming findings](https://github.com/WorldOfEpoch/codex-provider-compatibility-lab/blob/main/docs/compatibility-findings.md)
- [WHATWG server-sent events](https://html.spec.whatwg.org/multipage/server-sent-events.html#event-stream-interpretation)
