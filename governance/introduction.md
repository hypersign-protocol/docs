# Introduction

Hypersign Identity Network provides the facility of Governance, which provides opportunities to suggest changes in the blockchain. These suggestions to improve any aspect of the blockchain are expressed in the form of a proposal. A minimum deposit is needed (in $HID) to submit a proposal, and hence any user holding significant $HID can submit one of the following proposals:

- Simple Text Proposals
- Software Upgrade
- Blockchain Parameter Change
- Community Grants

Proposals status are of following types:

- **StatusDepositPeriod**
  - Time until necessary minimum deposit is made for a proposal
- **StatusVotingPeriod**
  - Time frame during which votes are accepted.
- **StatusPassed**
  - Proposal is passed and successfully executed
- **StatusRejected**
  - Proposal is rejected

A successful proposal requires a minimum participation from all stakeholders, known as Quoram. The value is 33.4% of total voting power

## Voting

Voting is essential is deciding whether a blockchain proposal will be accepted or rejected. Only Validators and their delegators have the ability to vote on proposals. There are four types of vote:

- **Yes**
  - Agreement on the proposal
- **No**
  - Disagreement on the proposal
- **Abstain** 
  - Refrains from voting on the proposal
- **No With Vote** 
  - Strongly Disagrees on the proposal with intention of discarding the propsal
  - If 33.4% or more votes `No With Veto`, the proposal is discarded and the deposit is burned, unlike in above scenarios where the deposit is refunded to the proposer.
  - This ensures that any spam proposal submission will result in proposer losing their deposit.

