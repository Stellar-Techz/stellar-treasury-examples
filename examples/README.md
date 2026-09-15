Stellar TreasuryKit

An open-source programmable treasury infrastructure toolkit for Stellar and Soroban.

Stellar TreasuryKit provides reusable smart-contract primitives, a TypeScript SDK, permission controls, spending limits, transaction proposals, events, and developer examples for building secure treasury systems on Stellar.

Instead of every Stellar application implementing its own treasury logic from scratch, TreasuryKit provides a common foundation that developers can integrate into their applications.

AI provides intelligence.
Soroban enforces rules.
Stellar settles transactions.

🚀 Overview

Managing blockchain treasury funds can become complicated when applications need:

Multiple authorized users or agents
Spending limits
Approved recipients
Asset restrictions
Transaction approvals
Emergency controls
Treasury activity monitoring
On-chain event tracking
Programmatic withdrawals
Automated or AI-assisted treasury operations

Stellar TreasuryKit aims to make these capabilities reusable.

The project provides a Soroban-based treasury contract together with a developer-friendly TypeScript SDK and practical examples.

Developers can use TreasuryKit to build:

DAOs
Creator payment systems
Grant distribution platforms
Payroll systems
Community treasuries
AI-powered treasury agents
Automated payment systems
DeFi applications
Startup/company treasuries
Multi-user financial applications
🎯 Problem

Many applications that manage funds need similar treasury functionality.

For example, an application may need to answer:

Who is allowed to withdraw funds?

How much can an authorized agent spend?

Which addresses can receive funds?

Which assets can the treasury hold?

Should a large transaction require approval?

How can the treasury be paused during an emergency?

How can off-chain applications monitor treasury activity?

Developers often end up rebuilding these mechanisms independently.

This can result in:

duplicated code
inconsistent permission systems
weak spending controls
difficult auditing
poor interoperability
more security-sensitive code

TreasuryKit provides reusable primitives for these problems.

💡 Solution

Stellar TreasuryKit introduces a programmable treasury layer for Stellar.

                ┌───────────────────────┐
                │      Application      │
                │                       │
                │ DAO / AI Agent /      │
                │ Payments / Grants     │
                └───────────┬───────────┘
                            │
                            ▼
                ┌───────────────────────┐
                │   TreasuryKit SDK     │
                │      TypeScript       │
                └───────────┬───────────┘
                            │
                            ▼
                ┌───────────────────────┐
                │ Soroban Treasury     │
                │       Contract        │
                │                       │
                │ Permissions           │
                │ Spending Limits       │
                │ Asset Rules            │
                │ Recipients             │
                │ Proposals              │
                │ Emergency Pause        │
                └───────────┬───────────┘
                            │
                            ▼
                ┌───────────────────────┐
                │       Stellar         │
                │       Network         │
                └───────────────────────┘

The key design principle is:

Applications decide what they want to do. TreasuryKit determines whether they are allowed to do it.

✨ Core Features
🏦 Programmable Treasury

Create an on-chain treasury controlled by configurable rules.

Supported capabilities include:

Treasury initialization
Deposits
Withdrawals
Treasury ownership
Authorized agents
Spending limits
Daily limits
Recipient allowlists
Asset restrictions
Emergency pause
Transaction proposals
Approval workflows
🔐 Permission Management

TreasuryKit uses role-based permissions.

Owner

The owner has full administrative control.

Possible responsibilities:

Add/remove agents
Configure spending limits
Add/remove recipients
Configure supported assets
Pause/unpause treasury
Transfer ownership
Approve administrative changes
Agent

An agent receives restricted permissions.

For example:

Agent
 ├── Can request withdrawal
 ├── Can execute approved transactions
 ├── Cannot change owner
 ├── Cannot modify security rules
 └── Cannot exceed spending limits

This makes it possible for an application or AI agent to interact with a treasury without receiving unrestricted control.

Soroban provides host-managed authorization primitives that TreasuryKit can build upon rather than creating an entirely separate authentication mechanism.

💰 Spending Limits

Treasury owners can configure limits for authorized agents.

Example:

Maximum transaction:
100 USDC

Daily spending limit:
500 USDC

Approved recipients:
- Payroll wallet
- Operations wallet
- Grant wallet

An agent attempting:

1,000 USDC

would be rejected by the treasury contract.

The important security principle is:

The agent cannot bypass the contract's rules.

👥 Recipient Allowlist

Treasury owners can define addresses that are allowed to receive funds.

Example:

Approved Recipients

Payroll      → G...
Operations   → G...
Grants       → G...
Marketing    → G...

A transaction directed to an unauthorized address can be rejected by the contract.

🪙 Asset Restrictions

TreasuryKit can support configurable asset policies.

For example:

Allowed Assets

USDC
XLM
EURC

The treasury can reject unsupported assets according to its configured policy.

This allows applications to establish clearer treasury rules.

📝 Transaction Proposals

TreasuryKit can support a proposal-based transaction flow.

                    ┌──────────────┐
                    │   Proposal   │
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │   Validate   │
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │   Approval   │
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │   Execute    │
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │   Stellar    │
                    └──────────────┘

This enables applications to implement approval workflows before funds move.

🤖 AI Agent Integration

AI is not required to use TreasuryKit.

Instead, AI can be an optional consumer of the toolkit.

For example:

User
 │
 ▼
AI Treasury Agent
 │
 ├── Analyze treasury
 ├── Detect unusual activity
 ├── Recommend transaction
 └── Create proposal
          │
          ▼
     TreasuryKit
          │
          ├── Check permissions
          ├── Check spending limit
          ├── Check recipient
          └── Check asset
                    │
                    ▼
                 Stellar

This separation is important.

The AI should not directly control treasury funds.

Instead:

AI recommends or requests an action. TreasuryKit enforces the rules.

This makes TreasuryKit useful for AI-powered applications without making the entire infrastructure dependent on a particular AI provider.

📡 On-Chain Events

TreasuryKit exposes standardized contract events for important treasury activity.

Example events:

TreasuryCreated
Deposit
Withdrawal
AgentAdded
AgentRemoved
LimitUpdated
RecipientAdded
RecipientRemoved
ProposalCreated
ProposalApproved
ProposalExecuted
TreasuryPaused
TreasuryUnpaused

Off-chain applications can consume these events to build:

dashboards
notifications
analytics
accounting systems
monitoring services
AI monitoring agents

Stellar supports contract events that off-chain applications can monitor, making event-driven treasury infrastructure a natural fit for the ecosystem.

🧩 TypeScript SDK

TreasuryKit will provide a TypeScript SDK to simplify interaction with the Soroban contracts.

Example:

import { TreasuryClient } from "@stellar-treasury-kit/sdk";

const treasury = new TreasuryClient({
  contractId: "CONTRACT_ID",
  rpcUrl: "SOROBAN_RPC_URL",
  network: "testnet",
});
Deposit
await treasury.deposit({
  asset: "USDC",
  amount: "100",
});
Withdraw
await treasury.withdraw({
  asset: "USDC",
  amount: "50",
  recipient: "G...",
});
Add Agent
await treasury.addAgent({
  address: "G...",
});
Configure Spending Limit
await treasury.setSpendingLimit({
  agent: "G...",
  asset: "USDC",
  amount: "500",
});
Add Recipient
await treasury.addRecipient({
  address: "G...",
});
Pause Treasury
await treasury.pause();

The SDK is intended to hide repetitive contract interaction details while keeping the underlying Soroban functionality accessible.

🏗️ Architecture
                    Stellar TreasuryKit
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
     Soroban          TypeScript        Examples
     Contracts           SDK              Apps
          │                │                │
          │                │                │
          ▼                ▼                ▼
     TreasuryVault    TreasuryClient    AI Agent
          │                               DAO
          │                               Grants
          │                               Payments
          │
          ▼
       Stellar
📁 Complete Project Structure
stellar-treasury-kit/
│
├── contracts/
│   │
│   └── treasury/
│       │
│       ├── src/
│       │   ├── lib.rs
│       │   ├── contract.rs
│       │   ├── storage.rs
│       │   ├── errors.rs
│       │   ├── events.rs
│       │   ├── types.rs
│       │   └── access.rs
│       │
│       ├── tests/
│       │   ├── treasury_test.rs
│       │   ├── permissions_test.rs
│       │   ├── limits_test.rs
│       │   ├── recipients_test.rs
│       │   ├── assets_test.rs
│       │   ├── proposals_test.rs
│       │   ├── pause_test.rs
│       │   └── security_test.rs
│       │
│       ├── Cargo.toml
│       └── Makefile
│
├── sdk/
│   │
│   ├── src/
│   │   ├── client.ts
│   │   ├── treasury.ts
│   │   ├── transactions.ts
│   │   ├── proposals.ts
│   │   ├── permissions.ts
│   │   ├── events.ts
│   │   ├── assets.ts
│   │   ├── errors.ts
│   │   ├── types.ts
│   │   └── index.ts
│   │
│   ├── tests/
│   │   ├── client.test.ts
│   │   ├── treasury.test.ts
│   │   ├── permissions.test.ts
│   │   └── proposals.test.ts
│   │
│   ├── package.json
│   ├── tsconfig.json
│   └── README.md
│
├── examples/
│   │
│   ├── basic-treasury/
│   │   ├── README.md
│   │   └── src/
│   │
│   ├── ai-agent/
│   │   ├── README.md
│   │   └── src/
│   │
│   ├── dao-treasury/
│   │   ├── README.md
│   │   └── src/
│   │
│   ├── recurring-payments/
│   │   ├── README.md
│   │   └── src/
│   │
│   └── grant-distribution/
│       ├── README.md
│       └── src/
│
├── scripts/
│   ├── build.ts
│   ├── deploy.ts
│   ├── initialize.ts
│   └── upgrade.ts
│
├── docs/
│   │
│   ├── getting-started.md
│   ├── architecture.md
│   ├── contract-api.md
│   ├── sdk.md
│   ├── permissions.md
│   ├── spending-limits.md
│   ├── proposals.md
│   ├── events.md
│   ├── security.md
│   ├── deployment.md
│   ├── testing.md
│   └── contributing.md
│
├── .github/
│   │
│   ├── workflows/
│   │   ├── test.yml
│   │   ├── contract.yml
│   │   └── release.yml
│   │
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   ├── feature_request.md
│   │   └── security_issue.md
│   │
│   └── PULL_REQUEST_TEMPLATE.md
│
├── .env.example
├── .gitignore
├── Cargo.toml
├── Cargo.lock
├── package.json
├── pnpm-workspace.yaml
├── LICENSE
├── README.md
├── CONTRIBUTING.md
├── SECURITY.md
└── CHANGELOG.md

The contract layout follows the general Rust workspace approach used in Stellar's Soroban tooling, while separating the reusable SDK, examples, documentation, and deployment tooling.

🔧 Technology Stack
Smart Contracts
Rust
Soroban SDK
WebAssembly
Stellar Network

Soroban smart contracts are currently written in Rust and compiled to WebAssembly for deployment.

SDK
TypeScript
Stellar SDK
Soroban RPC
Node.js
Testing
Rust unit tests
Soroban local testing
TypeScript tests
Integration tests
Developer Tooling
Stellar CLI
Cargo
Node.js
pnpm/npm
GitHub Actions
🔒 Security Model

Security is a core part of TreasuryKit.

The contract should enforce rules on-chain, rather than trusting an off-chain API.

Example

Suppose an AI agent requests:

Transfer:
5,000 USDC

Recipient:
GXYZ...

The contract checks:

Is agent authorized?
        │
        ├── No → Reject
        │
        ▼
Is asset allowed?
        │
        ├── No → Reject
        │
        ▼
Is recipient approved?
        │
        ├── No → Reject
        │
        ▼
Is amount within limit?
        │
        ├── No → Reject
        │
        ▼
Does treasury have enough funds?
        │
        ├── No → Reject
        │
        ▼
      Execute

This creates a security boundary between applications and treasury funds.

🛡️ Emergency Controls

Treasury owners should be able to pause sensitive treasury operations.

Example:

Normal Mode
     │
     ▼
Treasury Operations
     │
     ▼
Suspicious Activity
     │
     ▼
Pause Treasury
     │
     ▼
Investigate
     │
     ▼
Unpause

The pause mechanism should be carefully scoped so that emergency controls cannot accidentally create a permanent lockout.

🧪 Testing Strategy

TreasuryKit should prioritize negative/security tests rather than only testing successful transactions.

Contract tests
✓ Initialize treasury
✓ Deposit funds
✓ Withdraw funds
✓ Add agent
✓ Remove agent
✓ Configure limit
✓ Reject excessive transaction
✓ Add recipient
✓ Remove recipient
✓ Reject unauthorized recipient
✓ Add supported asset
✓ Reject unsupported asset
✓ Create proposal
✓ Approve proposal
✓ Execute proposal
✓ Reject unauthorized execution
✓ Pause treasury
✓ Reject restricted action while paused
✓ Unpause treasury
✓ Transfer ownership

Authorization behavior should be explicitly tested because Soroban provides authorization mechanisms that can be exercised and mocked in contract tests.

🚀 Getting Started
Prerequisites

Install:

Rust
Cargo
Stellar CLI
Node.js
npm/pnpm

Check your installation:

rustc --version
cargo --version
stellar --version
node --version
Clone Repository
git clone https://github.com/YOUR_USERNAME/stellar-treasury-kit.git

cd stellar-treasury-kit
Build Contracts
stellar contract build
Run Contract Tests
cargo test
Install SDK
cd sdk

npm install
Build SDK
npm run build
🌐 Network Support

TreasuryKit should support:

Development
     │
     ▼
Local Testing
     │
     ▼
Stellar Testnet
     │
     ▼
Stellar Mainnet

Development should begin on Testnet before any production deployment.

Stellar's documentation also recommends beginning smart-contract development and testing on Testnet.

📚 Documentation

Documentation will be organized into the following areas:

Documentation	Purpose
Getting Started	Install and run TreasuryKit
Architecture	Understand the system
Contract API	Soroban contract functions
SDK	TypeScript integration
Permissions	Roles and authorization
Spending Limits	Treasury spending controls
Proposals	Approval workflow
Events	Monitoring treasury activity
Security	Security model and considerations
Deployment	Testnet/Mainnet deployment
Testing	Contract and SDK testing
Contributing	Contributor guide
🧑‍💻 Example Use Cases
1. AI Treasury Agent

An AI agent monitors treasury activity and proposes transactions.

AI
 │
 ├── Analyze
 ├── Detect
 ├── Recommend
 │
 ▼
TreasuryKit
 │
 ├── Validate
 ├── Authorize
 └── Enforce Limits
 │
 ▼
Stellar
2. DAO Treasury

A DAO can use TreasuryKit to manage community funds.

DAO Members
     │
     ▼
Governance
     │
     ▼
Treasury Proposal
     │
     ▼
Approval
     │
     ▼
TreasuryKit
     │
     ▼
Stellar
3. Grant Distribution

Organizations can distribute grants using predefined treasury rules.

Grant Pool
    │
    ▼
TreasuryKit
    │
    ├── Recipient verification
    ├── Spending rules
    └── Distribution
           │
           ▼
       Recipients
4. Recurring Payments

Applications can build recurring payment workflows on top of the treasury infrastructure.

Examples:

Payroll
Contributor payments
Creator payments
Subscription payouts
Community rewards
🔌 Extensibility

TreasuryKit is designed as infrastructure rather than a single application.

Applications can build additional services around the core contract.

                 TreasuryKit
                      │
       ┌──────────────┼──────────────┐
       │              │              │
       ▼              ▼              ▼
    AI Agent         DAO         Payments
       │              │              │
       ▼              ▼              ▼
   Monitoring      Governance     Payroll

The core treasury contract remains focused on secure fund management while applications provide domain-specific logic.

🗺️ Roadmap
Phase 1 — Core Treasury

Treasury initialization

Deposit functionality

Withdrawal functionality

Owner permissions

Agent permissions

Basic events

Unit tests

Phase 2 — Security Controls

Spending limits

Daily limits

Recipient allowlist

Asset restrictions

Emergency pause

Ownership management

Security-focused tests

Phase 3 — Proposal System

Create proposal

Proposal validation

Approval workflow

Proposal execution

Proposal expiration

Proposal events

Phase 4 — TypeScript SDK

TreasuryClient

Transaction helpers

Permission helpers

Proposal helpers

Event utilities

Error handling

SDK documentation

Phase 5 — Examples

Basic treasury

AI treasury agent

DAO treasury

Recurring payments

Grant distribution

🔮 Future Expansion

TreasuryKit is intentionally designed so additional treasury capabilities can be added without changing its core purpose.

1. Multi-Signature Treasury

Support multiple administrators for sensitive operations.

Example:

Treasury
   │
   ├── Owner A
   ├── Owner B
   └── Owner C

2 of 3 approvals required

This would make TreasuryKit more suitable for organizations and DAOs.

2. Advanced Role-Based Permissions

Expand the permission system beyond Owner and Agent.

Potential roles:

OWNER
ADMIN
OPERATOR
AGENT
AUDITOR
VIEWER

Different roles could have different capabilities.

3. AI Risk Monitoring

Add optional AI-powered monitoring services.

The monitoring system could analyze:

transaction frequency
transaction size
unusual recipients
unusual asset movements
spending patterns
treasury balance changes

The AI would not directly control the treasury.

Instead:

Blockchain Activity
        │
        ▼
Monitoring Engine
        │
        ▼
Risk Analysis
        │
        ▼
Alert / Recommendation
4. Treasury Health Score

Applications could calculate a treasury health score based on configurable metrics.

Example:

Treasury Health

Liquidity       ████████░░ 80%
Spending Risk   ██████░░░░ 60%
Diversification ███████░░░ 70%
Activity        █████████░ 90%

Overall Score: 75/100

This would remain an off-chain analytics layer rather than being required by the core contract.

5. Recurring Payment Engine

A future service could provide reusable payment scheduling.

Example:

Every month
      │
      ▼
Check treasury rules
      │
      ▼
Check available balance
      │
      ▼
Execute authorized payment
      │
      ▼
Emit event

Possible use cases:

Payroll
Creator payouts
Contributor rewards
Subscription payments
Grants
6. Treasury Analytics

Build a standard analytics layer around TreasuryKit events.

Potential metrics:

Total deposits
Total withdrawals
Current balance
Transaction volume
Agent activity
Spending by recipient
Spending by asset
Failed transactions
7. Notification Integrations

Treasury events could trigger notifications through:

Webhooks
Email
Telegram
Discord
Slack
Mobile notifications

Example:

Large Withdrawal
       │
       ▼
TreasuryKit Event
       │
       ▼
Monitoring Service
       │
       ├── Email
       ├── Telegram
       └── Discord
8. Multi-Treasury Management

Organizations could manage multiple treasuries from one application.

Organization
     │
     ├── Operations Treasury
     ├── Payroll Treasury
     ├── Grant Treasury
     └── Community Treasury
9. Cross-Application Treasury Standards

A long-term goal is to make TreasuryKit easier for different Stellar applications to integrate.

For example:

Application A
      │
      ├──────┐
             ▼
Application B → TreasuryKit
             ▲
      ┌──────┘
      │
Application C

The objective is to provide reusable infrastructure rather than forcing developers to adopt a specific frontend or application architecture.

10. Treasury Adapters

Future versions could provide adapters for common application patterns.

Potential adapters:

DAOAdapter
GrantAdapter
PayrollAdapter
CreatorAdapter
AIAgentAdapter
PaymentAdapter

These adapters would sit above the core TreasuryKit contract.

11. Developer Dashboard

A future optional dashboard could allow developers to:

Create a treasury
Configure permissions
Configure spending limits
Manage recipients
View transactions
Monitor events
Manage proposals
Inspect treasury health

The dashboard would be an optional interface, not a requirement for using the SDK.

12. Security Audit Support

As the project matures, TreasuryKit should pursue independent security review before encouraging production use with significant funds.

The Stellar ecosystem provides security resources for eligible Soroban projects, including the Soroban Audit Bank for qualifying SCF-funded projects.

🌍 Why Stellar TreasuryKit?

Treasury infrastructure is a foundational component for many blockchain applications.

Instead of creating another application that only solves one treasury use case, TreasuryKit focuses on reusable infrastructure.

                         TreasuryKit
                              │
       ┌──────────────────────┼──────────────────────┐
       │                      │                      │
       ▼                      ▼                      ▼
      DAOs                 AI Agents             Payments
       │                      │                      │
       ▼                      ▼                      ▼
    Grants                Automation             Payroll
       │                      │                      │
       └──────────────────────┼──────────────────────┘
                              │
                              ▼
                           Stellar

This makes the project useful across multiple categories of Stellar applications.

🤝 Contributing

Contributions are welcome.

Possible contribution areas include:

Soroban contract development
Rust testing
TypeScript SDK
Documentation
Examples
Developer tooling
Security testing
Analytics integrations
AI integrations

Please read:

CONTRIBUTING.md

before opening a pull request.

🔐 Security

TreasuryKit deals with financial infrastructure.

Do not use the project with production funds until the relevant contracts have been thoroughly tested and independently reviewed.

If you discover a security vulnerability, please follow the instructions in:

SECURITY.md

Do not publicly disclose exploitable vulnerabilities before they have been responsibly reported and addressed.

📜 License

This project is released under the Apache License 2.0.

See:

LICENSE

for the complete license.

⭐ Project Vision

Make secure, programmable treasury infrastructure a reusable building block for the Stellar ecosystem.

TreasuryKit is not intended to be another standalone treasury dashboard.

It is intended to become a developer building block that applications can use to safely manage funds, permissions, limits, approvals, and treasury workflows on Stellar.

🚀 Future Vision

The long-term vision is:

                  Stellar TreasuryKit
                          │
             ┌────────────┼────────────┐
             │            │            │
             ▼            ▼            ▼
          Contracts       SDK       Standards
             │            │            │
             └────────────┼────────────┘
                          │
                          ▼
                  Stellar Applications
                          │
       ┌──────────┬───────┼────────┬──────────┐
       ▼          ▼       ▼        ▼          ▼
      DAO       AI Agent Grants  Payroll   Payments

Build once. Secure the rules on-chain. Let many Stellar applications use the infrastructure.