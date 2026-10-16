# SocietyLedger

A multi-tenant expense-claim service for student societies, proposed for **CSCI3100 Fall 2026, Option C**.

**Course demonstration only.** Use fictional amounts, synthetic accounts and sample receipts. No real reimbursements, payments or CUHK-system integration.

## Current status

Proposal-stage repository, maintained as a solo course project. The application, automated tests and cloud deployment have not been implemented yet.

## Target users and roles

- **Member:** submit claims, track personal claims and revise rejected claims.
- **Officer:** review claims and view the simulated budget within the officer's society.

Roles are assigned through society memberships. Each society's private records and administrative permissions remain separate. Demo data will include at least two fictional societies and accounts for both roles.

## Planned workflow and acceptance criteria

1. **Submit:** a positive amount, description and sample receipt create a submitted claim in the member's society. Invalid input is rejected without saving.
2. **Review:** an authorized society officer may approve or reject a claim. Self-approval and approval beyond the available budget are rejected without changing data. Approval deducts the amount once; rejection records a reason.
3. **Revise:** only the claimant may revise a rejected claim and resubmit it. Approved claims cannot be edited.
4. **Track:** members see their own claims; officers see their society's queue and budget. Provide status filters and description search.

Every action must enforce authorization on the server, including direct URL and request access.

## Proposed design

- Ruby 3.4, Ruby on Rails 8.1 and PostgreSQL; exact patch versions will be pinned during implementation.
- Main entities: users, societies, memberships, claims and budget entries.
- Claim states: submitted, approved, rejected and revised.
- Store money as integer cents.
- Commit approval, budget deduction and the approval entry in one database transaction.
- Use row locks to prevent concurrent overspending and a unique claim reference to prevent duplicate approval deductions.

## Testing and deployment plan

- RSpec unit/request tests and Cucumber acceptance tests.
- BDD scenarios and TDD red-green-refactor iterations.
- Test validation, invalid state transitions, self-approval, insufficient funds, repeated/concurrent approvals, permissions and organization isolation.
- Target at least 80% application-code line coverage with SimpleCov.
- Run both test suites through GitHub Actions on pushes and pull requests.
- Deploy a separate cloud-hosted Rails application with persistent PostgreSQL, HTTPS and environment-based secrets.

Setup, database seeding, run/test/coverage commands, the deployed URL, demo accounts, CI evidence and known limitations will be documented once implemented.

## Work plan

| Dates (2026) | Planned outcome |
| --- | --- |
| Oct 17-30 | Schema, accounts, permissions, demo seeds, CI and initial deployment |
| Oct 31-Nov 13 | Submission, review, revision, search and filters |
| Nov 14-27 | Transactional safeguards, failure/isolation tests and coverage |
| Nov 28-Dec 11 | Usability fixes, reproducibility checks, documentation and demonstration video |

Final submission deadline: **December 11, 2026, 23:59 Hong Kong time**.

## AI and reused-material acknowledgement

ChatGPT/Codex assisted with initial project planning, acceptance criteria, proposal drafting and repository documentation. This acknowledgement will be updated to reflect subsequent assistance and any permitted reused material. The project author remains responsible for correctness, tests and originality.

The submitted proposal contains private student-identification details and is intentionally not committed to this public repository. No application code from another project is included in this initial repository.
