# Assignment 7 — HTTP Client and Resilience (hardest of the week)

**Day 7 · Tue 17 Nov (finish Wed 18)** · Difficulty: ★★★★★

## Purpose
Call an external API safely. This is the core skill behind tweet-audit (Gemini) and payment-gateway (flaky bank).

## Learn first (~1 h)
`java.net.http.HttpClient`, request/response, status codes, timeouts, retryable vs non-retryable errors (5xx/timeouts vs 4xx), exponential backoff with jitter, idempotency (why retrying a POST needs care).

## Tasks
### Task 1 — Simple GET
Call a public, keyless JSON API (e.g. a public test API of your choice). Print status and body.
### Task 2 — Parse the response
Map the JSON into a record with Jackson.
### Task 3 — Timeouts and errors
Set connect and request timeouts. Handle 4xx, 5xx and network failure with distinct messages.
### Task 4 — Retry with backoff + jitter (hardest)
Write a `RetryingClient` that retries only transient failures, with exponential backoff and jitter and a max-attempts cap. Test it with a mocked `HttpClient` (or a local fake server) that fails twice, then succeeds. Log each attempt.

**Evidence:** log output showing attempts and delays; passing test.

## Stretch (only if ahead)
Run 10 calls concurrently with `CompletableFuture` and a limit on parallel requests.

## What I built (own words)
> 

## Checklist
- [ ] T1  - [ ] T2  - [ ] T3  - [ ] T4  - [ ] Test passing  - [ ] Committed  - [ ] Write-up
