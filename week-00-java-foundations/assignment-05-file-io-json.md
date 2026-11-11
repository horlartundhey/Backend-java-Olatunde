# Assignment 5 — File I/O and JSON (mini tweet-audit)

**Day 5 · Sun 15 Nov** · Difficulty: ★★★☆☆

## Purpose
A small preview of Project 1: read structured data from disk, process it, write a CSV.

## Learn first (~1 h)
`java.nio.file` (`Path`, `Files`), reading and writing text, Maven dependencies, Jackson (`ObjectMapper`, mapping JSON to records), CSV escaping basics.

## Tasks
### Task 1 — Dependency
Add Jackson to `pom.xml`. Build succeeds.
### Task 2 — Read JSON
Create a sample `tweets.json` (10+ tweets, made up). Parse it into `List<Tweet>`.
### Task 3 — Write CSV
Write all tweets to `out.csv` with columns `tweet_url,deleted`.
### Task 4 — Filter pipeline (hardest)
Load criteria from a `criteria.json` (`forbidden_words`, etc.), flag matching tweets using your A3 `TweetEvaluator`, write only flagged ones to `flagged.csv`. Missing/invalid file → clear error. Add `*.csv` and your real data to `.gitignore`.

**Evidence:** input file, output file, run output.

## What I built (own words)
> 

## Checklist
- [ ] T1  - [ ] T2  - [ ] T3  - [ ] T4  - [ ] Committed  - [ ] Write-up
