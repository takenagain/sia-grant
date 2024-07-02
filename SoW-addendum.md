### Analysis of Current Progress vs. Original Statement of Work (SoW) Timelines

#### Phase 1: Scope of Work
**Original Timeline:**
- **Deadline:** February 9, 2024
- **Deliverable:** Completed scope document with clear breakdown and delegation of tasks for both teams.

**Progress:**
- The Scope of Work document was completed and delivered on time, meeting the initial deadline.

#### Phase 2: Development Phase
**Original Timeline:**
- **Development Environment and Testnet:**
  - **Deadline:** February 23, 2024
  - **Deliverable:** Documentation on establishing a "regtest"-like network and a persistent internal testnet for development and testing.
  
- **Test Coin Activation:**
  - **Deadline:** February 23, 2024
  - **Deliverable:** A test coin activated within the Komodo DeFi Framework for testing purposes.

- **Sia Consensus Model Testing:**
  - **Deadline:** Initial report by March 22, 2024
  - **Deliverable:** Document providing a brief description of tests performed on each newly added SpendPolicy and a general overview of all "v2" consensus.

**Progress:**
- **Development Environment and Testnet:**
  - The Docker test suite was established to run a custom walletd instance in the DeFi Framework CI.

- **Test Coin Activation:**
  - Test Coin Activation is now possible within `dev` branch of the DeFi Framework. This test coin is currently only capable of generating a Sia UnlockConditions based address and querying the balance via a walletd API instance. Additional Walletd API endpoints have been integrated into the DeFi Framework API, but they are unused as of now beyond CI and unit tests. 

- **Sia Consensus Model Testing:**
  - Initial testing and feedback have been ongoing, with issues identified and reported to the Sia team. However, the comprehensive initial report is still pending. The report can be expected to be delievered alongside the RC release of "Sia Rust" or shortly thereafter.

**Reasons for Delays:**
- Shifting development focus to address critical issues in the Sia Rust implementation and resolving blockers related to "index mode" and encoding bugs. The method for interpretting responses from the Walletd API now relies on Sia Rust ported types. This method allows for directly utiliizing the equivalent types of Sia Go from the Walletd API client within the DeFi Framework. This design decision neccesitates Sia Rust being prioritized prior to the HTTP client.

#### Phase 2: Continued
- **Informational Wallet Functionality:**
  - **Deadline:** June 21, 2024
  - **Deliverable:** Demonstration of SIA coin activation within Komodo Wallet, including receive, transaction history, checking balance, and checking confirmations.

**Progress:**
- Encountered undefined behaviors in encoding methods in Sia core, necessitating refactoring of the Sia Rust encoding.
- Significant progress was made in implementing the necessary data types and developing the API client within the DeFi Framework. However, full demonstration of all functionalities is pending.

**Reasons for Delays:**
- The design decision was made to utilize the fundamental types ported from Sia core within the HTTP client. The delayed availability of "index mode" from the Sia team influenced this design decision. We believe this is a fundamentally better method of handling HTTP responses within the Walletd API client than originally proposed. This method allows for easier porting of Go types to Rust. The types related to HTTP requests and responses should now function identically across both the Go and Rust implementations.

#### Future Milestones and Progress:

- **Sia Rust Library:**
  - **Deadline:** August 2, 2024
  - **Deliverable:** Demonstration of the “Sia Rust” library, including signing and sending transactions, along with developer documentation.

- **Interactive Wallet Functionality:**
  - **Deadline:** August 23, 2024
  - **Deliverable:** Full Sia wallet functionality including sending, receiving, generating new addresses, importing addresses, viewing wallet history within Komodo DeFi Framework.

- **Peer-to-Peer Swap Protocol:**
  - **Deadline:** September 27, 2024
  - **Deliverable:** Demonstration of peer-to-peer atomic swaps within Komodo Wallet.

**Progress:**
- We have the fundamentals neccesary to begin creating and signing both v1 and v2 transactions. However, we have not yet fully ported the types required to account for SiaFunds or file contract operations within our transactions.
- We still lack the ability to fully deserialize all V2 "Events". We still require deserialization of contract resolution events. This will be neccesary to provide the full history of users' addresses.
- The feasibility of directly importing existing Sia seeds will be assessed. If Sia seeds are not easily adaptable to the current DeFi Framework codebase, we will provide an import, migration or conversion tool within the DeFi framework API.
- The "Sia Rust" library will be reorganized to act as a standalone library. Any DeFi Framework logic will be seperated from this crate. 
- Numerous unit tests have been implemented in both Go and Rust. More advanced fuzzer based tests will be developed to ensure the true 1:1 port of Sia Go's logic to Rust.
