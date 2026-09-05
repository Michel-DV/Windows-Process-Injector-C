# Detection Notes: Remote-Thread Process Injection

This directory contains defensive material for analyzing the behavior demonstrated by the repository.

## ATT&CK mapping

- **T1055 — Process Injection**

## Useful telemetry

### Sysmon Event ID 8 — CreateRemoteThread

This is the most direct event for the technique demonstrated here. Review:

- `SourceImage`
- `TargetImage`
- `SourceProcessId`
- `TargetProcessId`
- `StartAddress`
- `StartModule`
- `StartFunction`

A remote thread is not automatically malicious. Legitimate security, accessibility, debugging, and application software can also create remote threads.

### Sysmon Event ID 10 — ProcessAccess

Useful fields include:

- source and target process identities;
- requested access rights;
- process ancestry;
- signer/reputation context;
- timing relative to Event ID 8.

The strongest signal is often the relationship between events rather than one event in isolation.

## Triage questions

1. Is the source process expected to interact with the target?
2. Is either image unsigned, newly written, or running from an unusual path?
3. Did ProcessAccess precede CreateRemoteThread by only a short interval?
4. Is the remote thread start address backed by a normal loaded module?
5. Does the same source process repeat the behavior against multiple unrelated targets?
6. Are there related file, process, or network events around the same timestamp?

## Detection engineering guidance

Start with a broad rule, collect examples from your own environment, then tune known-good source/target pairs. Avoid suppressing events solely because a process is signed; signed software can still be abused.

The included Sigma rule is intentionally broad and should be treated as a **hunting/detection starter**, not a production-ready block rule.
