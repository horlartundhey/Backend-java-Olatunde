# Assignment 3 — OOP: Classes, Interfaces, Enums, Records

**Day 3 · Fri 13 Nov** · Difficulty: ★★☆☆☆

## Purpose
Model real data the way Project 1 and Project 2 will need it.

## Learn first (~1 h)
Classes, constructors, encapsulation, `equals/hashCode/toString`, interfaces, enums with fields, records, immutability, `Optional`.

## Tasks
### Task 1 — A class
`Tweet` class: id, text, createdAt (`java.time.Instant`). Private fields, constructor, getters, `toString`.
### Task 2 — A record
Rewrite `Tweet` as a `record`. Write 3 lines on what changed and why.
### Task 3 — An enum with behaviour
`PaymentState` enum: PENDING, AUTHORIZED, CAPTURED, REFUNDED, VOIDED. Add a method `canTransitionTo(PaymentState)`.
### Task 4 — An interface (hardest)
Interface `TweetEvaluator { boolean shouldFlag(Tweet t); }`. Implement `KeywordEvaluator` and `LengthEvaluator`. A `main` runs both over a list of tweets.
**Evidence:** UML sketch (paper photo is fine) + code + output.

## What I built (own words)
> 

## Checklist
- [ ] T1  - [ ] T2  - [ ] T3  - [ ] T4  - [ ] Committed  - [ ] Write-up
