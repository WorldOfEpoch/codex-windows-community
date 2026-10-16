# Codex Windows community

A public place to document Codex-on-Windows problems, separate symptoms from causes, compare fixes, and learn from each other's results. Start with the [case index](cases/README.md).

The goal is simple: a person should be able to find their symptom, see what is actually known, try a scoped and reversible remedy when one exists, and report whether it worked on their version. Unresolved reports are useful too. A repeated error message is not enough to prove a shared cause.

This is an independent community project maintained by WorldOfEpoch. It is not official OpenAI support. It currently contains documentation and issue forms; it does not install software, modify settings, run cleanup, or start background services.

## Find a problem or contribute

| What you want to do | Start here |
| --- | --- |
| Find a known symptom | [Browse the case index](cases/README.md) |
| Report the same issue | Find the case's tracking issue and add your version and observations; the [report form](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml) also accepts a matching case ID |
| Report something new | [Open a problem report](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=bug_report.yml) |
| Propose a fix or add test results | [Open a fix contribution](https://github.com/WorldOfEpoch/codex-windows-community/issues/new?template=fix_proposal.yml) or submit a pull request |
| Correct a conclusion or add community notes | Comment with evidence on the relevant issue, or propose an edit to its case file |
| Work on model-provider compatibility code | [Codex provider compatibility lab](https://github.com/WorldOfEpoch/codex-provider-compatibility-lab) |

Please read [CONTRIBUTING](CONTRIBUTING.md) before attaching evidence. Use synthetic examples and summaries; keep real conversations, credentials, addresses, and raw diagnostic bundles private.

## What is recorded so far

The initial records come from a bounded investigation on October 16, 2026. They include a retired global model relay, its restart watcher, repeated Blender connector helpers, optional connector discovery failures, protocol risks, thread-read authorization errors, notification reconnects, and app-server WebSocket closures.

The investigation confirmed that a local relay could disrupt ordinary model requests. It did **not** establish that the relay caused every error. Some failures continued after its configuration was removed, and already-open clients still retained old settings. Each case records its own evidence and unresolved questions.

The historical Space Bunny integration remains retired. Reusing a lesson does not require restoring it. This project does not include its installer, credentials, private source, settings, or logs.

## How the project can grow

1. Collect small, reproducible reports with exact software versions and a clear symptom.
2. Separate matching symptoms from a confirmed common cause; maintain one case per problem with links between related cases.
3. Develop scoped fixes in the component that owns the problem, with a regression test and rollback instructions.
4. Record the exact versions and commits on which a fix was tested. Keep source review, synthetic tests, local verification, and upstream release fixes distinct.
5. Make setup, diagnosis, and recovery easier without adding hidden services or changing unrelated projects.

The case files are the maintained summaries. GitHub issues hold community discussion, additional environments, proposed explanations, and test results. A discussion or closed issue alone does not promote a case to a confirmed fix. The machine-readable [case index](cases/index.json) contains stable IDs and explicit status fields.

This is an initial case collection, not a complete historical inventory or a claim that every current Codex release has these problems. See [evidence levels and contribution rules](CONTRIBUTING.md).

Licensed under [MIT](LICENSE). Security-sensitive reports follow [SECURITY](SECURITY.md).
