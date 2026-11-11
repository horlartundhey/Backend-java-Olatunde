# Assignment 6 — Testing: JUnit 5 and Mockito

**Day 6 · Mon 16 Nov** · Difficulty: ★★★★☆

## Purpose
The path requires tests that never call paid external services. Learn to isolate dependencies.

## Learn first (~1 h)
JUnit 5 (`@Test`, assertions, `@ParameterizedTest`), arrange/act/assert, test doubles (stub vs mock), Mockito (`mock`, `when`, `verify`), designing code so dependencies are injected.

## Tasks
### Task 1 — First tests
Test `isPrime` and the grade calculator from A2.
### Task 2 — Exceptions
Assert your custom exception is thrown for bad input (`assertThrows`).
### Task 3 — Parameterized tests
Table of inputs/outputs for your evaluators from A3.
### Task 4 — Mock a dependency (hardest)
Refactor A5 so JSON loading sits behind an interface (e.g. `TweetSource`). Test the filter pipeline with a mocked `TweetSource`, with no file on disk. Verify the CSV writer receives the expected tweets.

**Evidence:** `mvn test` green screenshot; list of test names.

## What I built (own words)
> 

## Checklist
- [ ] T1  - [ ] T2  - [ ] T3  - [ ] T4  - [ ] Committed  - [ ] Write-up
