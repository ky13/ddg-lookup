---
name: ddg
description: Quick public-web lookup through ddgr (DuckDuckGo), answered from result snippets at minimum token cost.
disable-model-invocation: true
---

A **lookup**: one search, a short answer, done. The user invokes this to keep a quick question cheap, so the whole job is a single `ddgr` call and, rarely, one page read.

1. Turn the question into search terms and run exactly:

   ```sh
   ddgr --json --np -n 5 'search terms'
   ```

   Add `-t w`, `-t m`, or `-t y` when the answer depends on recent events (past week, month, year). If `ddgr` is missing, reply with the install command (`sudo apt install ddgr` on Debian/Ubuntu, `brew install ddgr` on macOS) and stop.

2. Answer from the `abstract` fields, copying numbers, versions, names, and dates exactly as the source writes them. Done when the reply is at most three lines plus the one URL the answer came from.

3. Only when no abstract answers it: read the single most promising URL and take just the needed fact from it. Done after that one page: reply with the answer and its URL, or say it wasn't found and list the top three titles with URLs.

Stay on the ddgr results for the whole lookup: no built-in web search tool, no subagents, no local file searches, no follow-up research. If the question turns out to need real investigation, say so in one line and let the user decide.
