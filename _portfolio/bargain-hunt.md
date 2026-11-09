---
title: Bargain Hunt in numbers
summary: An LLM pipeline that turns BBC Bargain Hunt subtitles into a dataset of every item bought and sold, and the stats behind it.
img: /assets/img/portfolio/bargain-hunt.png
order: 1
date: 2026-11-07
tags: [Data, LLMs, Python, Docker]
---

What did each team on *Bargain Hunt* buy, what did they pay, and what did it fetch at auction?
The show tells you, but only out loud. This project pulls those numbers out of the episodes
and turns them into an unofficial stats page: which categories make money, which experts'
teams do best, and the best finds and worst buys.

## How it works

1. **Fetch.** [`get_iplayer`](https://github.com/get-iplayer/get_iplayer) downloads only the
   subtitle files (no video) for episodes currently on iPlayer.
2. **Extract.** Each subtitle file becomes a timestamped transcript, which an OpenAI model
   turns into structured JSON: teams, items, prices paid and auction results. Every price
   keeps the transcript quotes it came from, so any number can be traced back to what was said.
3. **Check.** Each episode is sanity-checked automatically. Does each team have the right
   number of items, and do the item prices add up to the profit or loss announced on the show?
   Anything that doesn't is flagged for a manual look.
4. **Publish.** Results are flattened to a CSV and built into a single self-contained web page,
   with no external scripts, and deployed to Cloudflare Pages.

The whole pipeline reruns daily on a schedule. Episodes already extracted are skipped, so a
rerun only pays for new ones.

## Built to be careful

Everything runs in a locked-down Docker container. It runs as a normal user with no Linux
capabilities and a read-only filesystem, and can see only its own data folder. `get_iplayer`
is pinned to a fixed release and its hash is checked during the build. The publish step runs
in a separate throwaway container that never sees the OpenAI key, and contestant names stay
off the public page.
