---
title: RiskyClick
summary: A serverless pipeline that collects phishing feeds around the clock, building a history of malicious links to analyse.
order: 5
date: 2020-12-13
tags: [Security, Data, Python, AWS]
redirect_from: /portfolio/riskyclick
---

Phishing links don't last long. Most are taken down or abandoned within hours or days, so a list
of what's malicious *right now* says little about how phishing works over time. RiskyClick is
a project to collect those links continuously, keep a history, and analyse it: which domains,
hosts and patterns phishers rely on, and how that changes.

## How it works

1. **Ingest.** Scheduled AWS Lambda functions, deployed with the Serverless Framework, pull the
   public [OpenPhish](https://openphish.com) and [PhishTank](https://phishtank.org) feeds hourly
   and every 12 hours. ETag checks skip downloads when a feed hasn't changed.
2. **ETL.** Raw snapshots are parsed and deduplicated, then loaded into S3 as datasets
   partitioned by ingest date. For PhishTank, a running "current" database is kept, and each run
   outputs only the new entries.
3. **Enrich.** Domains are resolved to IP addresses over DNS-over-HTTPS, so links can be grouped
   by the infrastructure behind them, not just the URL.
4. **Analyse.** Jupyter notebooks explore the data: duplication between and within feeds, the
   most common words and keywords in phishing domains, and monthly snapshots of each feed.

The pipeline code has unit tests for each ingest, ETL and enrichment step, which run in CI on
every push.
