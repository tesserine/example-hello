# example-hello

A minimal, deliberately trivial repository for exercising the Tesserine agent ecosystem. Point an [agentd](https://github.com/tesserine/agentd) session at this repo's clone URL to verify that the stack — agentd, [runa](https://github.com/tesserine/runa), [groundwork](https://github.com/tesserine/groundwork), and the [base](https://github.com/tesserine/base) image — lights up end-to-end.

## Contents

- `hello.py` — a one-function Python module. A Tesserine session receives a request such as "add a `greet(name)` function," produces the change via the groundwork methodology, and completes cleanly.

## Usage

This is the canonical integration request, as named by
[commons ECOSYSTEM-RELEASE.md](https://github.com/tesserine/commons/blob/main/ECOSYSTEM-RELEASE.md):
**add a `greet(name)` function**.

1. Add this agent to your `agentd.toml` (adjust `base_image`,
   `methodology_dir`, and the credential source to your host; full config
   reference: [agentd README](https://github.com/tesserine/agentd#configuration)):

   ```toml
   [[agents]]
   name = "site-builder"
   base_image = "localhost/tesserine/base"
   methodology_dir = "../groundwork"
   repo = "https://github.com/tesserine/example-hello"

   [agents.command]
   argv = ["claude", "-p", "--dangerously-skip-permissions"]

   [[agents.credentials]]
   name = "ANTHROPIC_API_KEY"
   source = "AGENTD_ANTHROPIC_KEY"
   ```

2. With the daemon running, trigger the smoke-test session:

   ```sh
   agentd run site-builder --request 'add a `greet(name)` function'
   ```

## Pass criteria

The stack is operational when all of the following hold:

- `agentd run` reports outcome `success` (exit code `0` — see
  [commons EXIT-CODES.md](https://github.com/tesserine/commons/blob/main/EXIT-CODES.md)).
- A sealed audit record exists for the session
  (`<audit_root>/site-builder/<session_id>/` with `outcome` populated in
  `agentd/session.json` — format:
  [agentd audit-record reference](https://github.com/tesserine/agentd/blob/main/docs/audit-record.md)).
- The session's branch or PR on this repo adds a working `greet(name)` to
  `hello.py`.

Any other outcome label, an unsealed record, or a session that stops
blocked mid-protocol is a failed smoke test; diagnose from the audit
record.

## Scope

This repository is intentionally minimal. It exists to verify that the Tesserine ecosystem is operational — not to demonstrate its breadth. Additional `example-*` repositories will exercise richer scenarios (multi-file changes, review cycles, alternative methodology profiles) as they are developed.

## License

MIT. See [LICENSE](./LICENSE).
