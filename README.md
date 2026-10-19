# ddg-lookup

Cheap web lookups for coding agents. One [ddgr](https://github.com/jarun/ddgr) (DuckDuckGo) search, a three-line answer from the result snippets plus its source URL, and at most one page read when the snippets don't cover it. No paid search tool, no browser, no research spiral.

Two ways to use it:

- **`/skill:ddg <question>`** inside an agent session. Runs on that session's model and context, so it's convenient but costs what the session costs.
- **`q <question>`** from any shell. A separate one-shot [omp](https://github.com/can1357/oh-my-pi) run on Haiku with thinking off, only shell and file-read tools, no saved session, launched from `$HOME` so no project context loads. Measured at about 13K tokens of fixed context: roughly $0.03 for the first call, under a cent while the prompt cache is warm, 4 to 9 seconds.

```
$ q default HTTP monitoring port for nats-server
8222 is the conventional port; monitoring is off until you set `http_port: 8222` or pass `-m 8222`.

https://docs.nats.io/learn/monitoring/monitoring-endpoints
```

## Install

Requires `ddgr` (`sudo apt install ddgr` or `brew install ddgr`).

```sh
git clone https://github.com/ky13/ddg-lookup ~/code/ddg-lookup

# the skill, for omp
ln -s ~/code/ddg-lookup/skills/ddg ~/.omp/agent/skills/ddg

# q, needs omp
ln -s ~/code/ddg-lookup/bin/q ~/.local/bin/q
```

`q` finds the skill next to itself through the symlink. Override with `Q_SKILL=/path/to/SKILL.md`, and pick another model with `Q_MODEL`.

The skill uses the standard `SKILL.md` format with `disable-model-invocation: true`, so it only runs when you call it and adds nothing to normal sessions. Other agents that read that format, such as Claude Code (`~/.claude/skills/ddg/`), should load it too, but only omp has been tested.

## Caveats

- Small models occasionally garble a fact while copying it (one test turned version 8.2.8 into "0.82.8" before the skill told it to copy facts verbatim). Treat answers to anything important as a lead to check.
- `ddgr` scrapes DuckDuckGo's HTML results, so it can break when DuckDuckGo changes its page.

## License

MIT
