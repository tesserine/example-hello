# example-hello

A minimal, deliberately trivial repository for exercising the Tesserine agent ecosystem. Point an [agentd](https://github.com/tesserine/agentd) session at this repo's clone URL to verify that the stack — agentd, [runa](https://github.com/tesserine/runa), [groundwork](https://github.com/tesserine/groundwork), and the [base](https://github.com/tesserine/base) image — lights up end-to-end.

## Contents

- `hello.py` — a one-function Python module. A Tesserine session receives a request such as "add a `greet(name)` function," produces the change via the groundwork methodology, and completes cleanly.

## Usage

Configure an agentd profile to clone this repo and deliver a request artifact into the session workspace. The exact injection mechanism is profile-dependent; see [agentd's documentation](https://github.com/tesserine/agentd) for profile configuration.

Clone URL:

```
https://github.com/tesserine/example-hello
```

## Scope

This repository is intentionally minimal. It exists to verify that the Tesserine ecosystem is operational — not to demonstrate its breadth. Additional `example-*` repositories will exercise richer scenarios (multi-file changes, review cycles, alternative methodology profiles) as they are developed.

## License

MIT. See [LICENSE](./LICENSE).
