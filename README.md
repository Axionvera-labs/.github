<div align="center">

# Axionvera Labs

### Programmable rewards for businesses, fintechs, startups, and the agents who help them grow.

Create reward campaigns, define qualifying actions, verify agent activity, and settle payouts on Stellar.

<br />

![Built on Stellar](https://img.shields.io/badge/Built%20on-Stellar-7B61FF?style=for-the-badge)
![Smart Contracts](https://img.shields.io/badge/Smart%20Contracts-Soroban-000000?style=for-the-badge)
![SDK](https://img.shields.io/badge/SDK-TypeScript-3178C6?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active%20Development-0E8A16?style=for-the-badge)

<br />

**Create campaigns. Verify activity. Reward agents.**

</div>

---

## What is Axionvera?

Axionvera is a programmable rewards platform for organisations that rely on agents, partners, referrers, field teams, ambassadors, or contractors to drive growth.

Instead of running incentive programmes on spreadsheets, manual approvals, and fragmented payouts, businesses use Axionvera to:

- **Create & fund campaigns** with explicit budgets, timelines, and per-agent caps
- **Define activation rules** linking measurable milestones to reward amounts
- **Authorise trusted verifiers** (ops teams, managers, or backend services) to confirm off-chain or on-chain activity
- **Allocate & settle rewards** transparently on Stellar, with on-chain events and self-serve claiming for agents

---

## Repositories

| Repository | Stack | Role |
| --- | --- | --- |
| [**axionvera-network**](https://github.com/Axionvera-labs/axionvera-network) | Rust · Soroban | Campaign, Vault, and Rewards smart contracts, interface schemas, and deployment tooling |
| [**axionvera-sdk**](https://github.com/Axionvera-labs/axionvera-sdk) | TypeScript · React | `@axionvera/core` and `@axionvera/react` SDK for contract reads/writes, typed events, and wallet signing |
| [**axionvera-dashboard**](https://github.com/Axionvera-labs/axionvera-dashboard) | Next.js · TypeScript | Web dashboard for campaign and vault management, reward tracking, and Freighter wallet flows |

---

## How It Works

```text
Business / Fintech / Startup
  ├── Creates & funds campaign (budget, rules, per-agent cap)
  └── Authorises trusted verifiers
              │
              ▼
    Agent completes qualifying action
              │
              ▼
    Verifier confirms activity  ──▶  Smart contract allocates reward
                                                  │
                                                  ▼
                                     Agent claims reward on Stellar
```

### Example: Merchant Acquisition

A fintech launches **Merchant Growth Q4** with a 10,000 USDC budget, a 500 USDC per-agent cap, and three activation rules:

| Activation Rule | Reward |
| --- | --- |
| Verified Merchant Onboarded | 5 USDC |
| First 10 Transactions | 10 USDC |
| Premium Merchant Activated | 25 USDC |

When an agent onboards a merchant and an authorised verifier (e.g., an operations API or regional manager) confirms it, the contract allocates 5 USDC to the agent's claimable balance. The agent can accumulate allocations over time and claim directly on Stellar.

---

## Core Concepts

| Primitive | How It Works |
| --- | --- |
| **Campaigns** | Self-contained programmes with an admin, reward asset, budget, schedule, per-agent cap, and lifecycle controls (Active → Pause / Resume → Close). |
| **Activation Rules** | Named milestones mapped to fixed reward amounts so payout logic is explicit and auditable. |
| **Verifiers** | Permissioned roles separated from agents. Qualifying actions do not need to happen on-chain — a trusted verifier confirms them before allocation. |
| **Campaign Accounting** | Explicit on-chain separation of Funded Amount, Allocated Rewards, Claimed Rewards, and Unused Funds (withdrawable after close). |

---

## Who It's For & Use Cases

| Segment | Example Incentive Programmes |
| --- | --- |
| **Fintechs** | Merchant onboarding, customer activation, KYC completion, transaction-volume incentives |
| **Businesses & Field Sales** | Verified sales milestones, retail/product distribution, regional partner targets |
| **Startups** | Customer referrals, affiliate conversions, ambassador and community growth campaigns |
| **Agent & Gig Networks** | Verified task completion and performance-based payouts across distributed teams |

---

## Why Stellar & Soroban?

For Axionvera, Stellar is the infrastructure beneath the experience, not the experience itself. Businesses focus on who gets rewarded, for what action, how much, and who verifies it, while Stellar and Soroban provide:

- Fast, low-cost global settlement with native digital asset support (e.g. USDC)
- Deterministic smart-contract accounting and access control via Soroban
- Structured on-chain events for activity feeds, dashboards, analytics, and audit trails

---

## Architecture & Current Coverage

```text
  Business & Agent Apps (axionvera-dashboard)
                    │
                    ▼
        TypeScript SDK (axionvera-sdk)
                    │
                    ▼
   Soroban Smart Contracts (axionvera-network)
                    │
                    ▼
            Stellar / Soroban
```

- **Smart Contracts:** Full Campaign contract lifecycle — 21 public methods (9 reads, 12 writes) and 12 typed lifecycle events, validated end-to-end on Stellar Testnet.
- **SDK (`@axionvera/core` & `@axionvera/react`):** Typed contract clients, live Soroban reads/writes, simulation, wallet signing, contract error handling, RPC event queries/decoding, and React hooks.

<details>
<summary>View full Campaign contract methods (21) &amp; events (12)</summary>

**Reads (9)**

`get_campaign` · `get_activation_rule` · `is_verifier` · `claimable_reward` · `agent_total_earned` · `available_unused_funds` · `is_initialized` · `protocol_admin` · `next_campaign_id`

**Writes (12)**

`initialize` · `create_campaign` · `fund_campaign` · `add_activation_rule` · `add_verifier` · `remove_verifier` · `pause_campaign` · `resume_campaign` · `close_campaign` · `withdraw_unused_funds` · `verify_and_allocate_reward` · `claim_reward`

**Events (12)**

campaign initialized · campaign created · campaign funded · activation rule added · verifier added · verifier removed · reward allocated · reward claimed · campaign paused · campaign resumed · campaign closed · unused funds withdrawn

</details>

---

## Roadmap

| Phase | Focus | Highlights |
| --- | --- | --- |
| **Phase 1 — Campaign Infrastructure** (Current) | Protocol & SDK | Soroban Campaign contract, typed Core/React SDK, live reads/writes, event decoding, Testnet end-to-end validation |
| **Phase 2 — Product Experience** | Applications | Business campaign dashboard, agent claim portal, verifier workflows, campaign analytics, smoother wallet onboarding |
| **Phase 3 — Integrations** | Ecosystem | Business APIs, webhooks & event delivery, backend verification hooks, fintech & payment integrations |
| **Phase 4 — Production Growth** | Scale | Mainnet deployment, security reviews, production business & agent-network pilots |

---

## Engineering Principles

- **Product first** — Every technical layer exists to support a real business workflow, not blockchain complexity for its own sake.
- **Clear accounting** — Funding, allocations, claims, and unused balances are always explicit on-chain.
- **Controlled verification** — Only authorised verifiers can approve reward-triggering actions.
- **Tested on Stellar** — Critical lifecycles are verified against Stellar Testnet in addition to unit and integration tests.

---

<div align="center">

**Reward the people who help your business grow.**

Create campaigns. Verify meaningful activity. Reward agents transparently.

**Axionvera — programmable agent rewards, powered by Stellar.**

</div>
