# Uniswap V2 Core: Audit Engagement Scoping

A mock pre-audit scoping package for [Uniswap v2-core](https://github.com/Uniswap/v2-core), written the way a security engagement would be scoped before kickoff: what's in scope, where the risk is, how long it should take, how it would be delivered, and what needs answering from the client first.

> Personal practice exercise. Not affiliated with Uniswap Labs or any audit firm, and not an audit. No findings are claimed.

**Reviewed commit:** [`6a9e7c97860676e0992f22a49665760444c1cdf5`](https://github.com/Uniswap/v2-core/tree/6a9e7c97860676e0992f22a49665760444c1cdf5)
**Raw metrics:** [metrics.md](./metrics.md) (generated with Consensys `solidity-code-metrics`)

---

## 1. Overview

Uniswap v2-core is the minimal on-chain layer of Uniswap V2: a factory that deploys one pool per token pair, and pair contracts that hold liquidity and execute swaps against the constant product formula `x * y = k`. It also exposes cumulative price accumulators used by other protocols as TWAP oracles.

The user-facing Router lives in a separate repo (v2-periphery) and is **out of scope** unless the client confirms otherwise (see Open Questions).

## 2. Scope

| Contract | Type | nSLOC | Complexity | Notes |
|---|---|---|---|---|
| `UniswapV2Pair.sol` | Deployable | 167 | 184 | Core logic: swap, mint, burn, oracle, protocol fee. Highest risk |
| `UniswapV2ERC20.sol` | Base (LP token) | 79 | 61 | ERC-20 + EIP-2612 permit, assembly for chain ID, ecrecover |
| `UniswapV2Factory.sol` | Deployable | 40 | 46 | Pair creation via create2, fee switch admin |
| `libraries/Math.sol` | Library | 18 | 5 | `min`, Babylonian `sqrt` |
| `libraries/SafeMath.sol` | Library | 12 | 4 | Overflow checks (pre-0.8 compiler) |
| `libraries/UQ112x112.sol` | Library | 10 | 4 | Fixed-point math for price accumulators |
| **Total** | | **326** | **304** | |

**Out of scope:** `contracts/interfaces/*`, test files, v2-periphery (Router, libraries), deployment scripts.

**Key characteristics**
- Compiler pinned to `=0.5.16` (no built-in overflow checks)
- 18 public/external entry points, 0 payable
- 2 inline assembly blocks, `create2` deployment, `ecrecover` signature handling
- No upgradeability, no pause, no admin control over user funds

## 3. Access Control

| Function | Who can call | Risk note |
|---|---|---|
| `Factory.createPair` | Anyone | Permissionless by design |
| `Factory.setFeeTo` / `setFeeToSetter` | `feeToSetter` only | Only privileged role in the system |
| `Pair.initialize` | Factory only, once | Must not be callable twice |
| `Pair.mint` / `burn` / `swap` / `skim` / `sync` | Anyone, behind `lock` | Reentrancy guarded |
| `ERC20.permit` | Anyone with a valid signature | Signature replay surface |

Centralization risk is low: the only admin power is redirecting the protocol fee.

## 4. Risk Areas

Prioritized for auditor focus.

1. **Invariant and rounding math** in `swap`, `mint`, `burn`, `_mintFee`. Any error here can drain pools.
2. **Optimistic transfers and flash swaps.** `swap` sends tokens before payment and calls back into arbitrary code (`uniswapV2Call`). Safety depends entirely on the `lock` modifier and the final fee-adjusted `k` check.
3. **Oracle integrity.** `getReserves()` spot values are manipulable within one transaction; the cumulative price accumulators are the intended oracle. Overflow of accumulators and `uint32` timestamps is intentional and must be verified as safe.
4. **Non-standard tokens.** Fee-on-transfer, rebasing and no-return-value tokens. Handled via balance diffs, `_safeTransfer`, `skim` and `sync`, but needs explicit test coverage.
5. **First-depositor / share inflation.** Mitigated by burning `MINIMUM_LIQUIDITY` (1000 LP). Confirm the mitigation holds for low-decimal tokens.
6. **Non-atomic mint/burn.** Tokens transferred in one tx and claimed in another can be front-run. Designed to be used atomically via the Router, so integration assumptions need documenting.
7. **Permit and chain forks.** `DOMAIN_SEPARATOR` is computed once at deploy, so signatures may be replayable on a forked chain.
8. **Storage packing and casts.** Reserves stored as `uint112`, overflow guarded in `_update`.
9. **Legacy compiler.** Review known 0.5.16 compiler bugs against the code paths used.

## 5. Effort Estimate

| Activity | Effort |
|---|---|
| Kickoff + architecture walkthrough | 0.5 day |
| Manual review, 2 auditors in parallel | 2 x 5 days |
| Invariant / fuzz testing on swap and mint/burn math | 2 days (within the above) |
| Report drafting + internal quality review | 2 days |
| Fix review | 1 to 2 days |
| **Total** | **~2 auditor-weeks + fix review, ~3 calendar weeks** |

**Reasoning:** 326 nSLOC is small, but this code secures large TVL, contains custom fixed-point math and an unusual optimistic transfer + callback pattern. Two auditors gives independent coverage of the Pair contract, which holds over half the code and nearly all of the risk. If the client adds v2-periphery to scope, re-estimate before kickoff.

## 6. Delivery Plan

| Week | Milestone | Gate |
|---|---|---|
| 0 | Scope confirmed, SOW signed, repo access + commit frozen, kickoff call | **Go/no-go:** scope, commit hash and open questions resolved |
| 1 | Manual review + invariant testing | Mid-week check-in with client engineering, early critical issues shared immediately |
| 2 | Draft report delivered, client fix window opens | **Go/no-go:** all Critical/High acknowledged by client |
| 3 | Fix review, final report, publication | **Go/no-go:** fixes verified, client approves publication |

**Change control:** any scope addition after kickoff (new contracts, new commit) goes through a change order with a revised estimate and timeline.

### RASCI

| Activity | Program Manager | Lead Auditor | Auditor 2 | Client Eng Lead | Client Exec |
|---|---|---|---|---|---|
| Scope + SOW | R/A | C | | C | S |
| Kickoff | R/A | S | S | C | I |
| Review + testing | I | R/A | R | C | |
| Status reporting | R/A | S | | I | I |
| Fixes | I | C | C | R/A | I |
| Fix review + final report | A | R | R | C | I |
| Publication | R/A | C | | C | S |

R = Responsible, A = Accountable, S = Supportive, C = Consulted, I = Informed

## 7. RAID Log

| Type | Item | Impact | Owner | Mitigation / Status |
|---|---|---|---|---|
| Risk | Client pushes new commits mid-audit | Scope creep, delay | PM | Freeze commit at kickoff, changes via change order |
| Risk | Router left out of scope but most integration risk lives there | Incomplete coverage | PM | Flag in report, offer follow-up engagement |
| Risk | Critical finding late in week 1 | Fix window too short | Lead Auditor | Share criticals immediately, don't wait for report |
| Assumption | Only the 6 listed files are in scope | Estimate validity | PM | Confirm in SOW |
| Assumption | Client provides an engineer for questions within 24h | Auditor blocking | Client Eng Lead | Agree response SLA at kickoff |
| Issue | Repo has no in-repo spec of supported token types | Ambiguous expected behavior | PM | Raised as Open Question #2 |
| Dependency | Repo access and frozen commit hash | Can't start | Client Eng Lead | Required before go/no-go week 0 |
| Dependency | Client availability for fix window in week 2 | Timeline slip | Client Exec | Confirm dates at kickoff |

## 8. Open Questions for the Client

1. Is v2-periphery (Router) in scope? Most real-world integration issues happen there.
2. Which token types must be supported: fee-on-transfer, rebasing, low-decimal?
3. Will the protocol fee be on at launch, and is `feeToSetter` an EOA or a multisig?
4. Any planned deviations from the 0.3% fee or `MINIMUM_LIQUIDITY`?
5. Target deployment chains? (affects the permit chain-fork risk)
6. Is there an existing test suite or spec the auditors should treat as source of truth?
