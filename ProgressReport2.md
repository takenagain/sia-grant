# Progress Report #2

As per the Scope of Work document, a test report regarding the manual testing processes of Sia's new "v2" consensus mechanisms is expected as of today. Much of the time in the past weeks was dedicated to establishing the "Sia Rust" library. This task was identified as a neccesary step towards further in-depth consensus mechanism testing. A test report will be produced in the coming weeks. 

## Komodo Testnet walletd Rebase

The Komodo testnet branch has been rebased to SiaFoundation's latest master branch after previously being some weeks behind due to using the "its-happening" branch as upstream.

This was identified as a critical step forward as the DeFi Framework will require use of walletd API's newly introduced "indexer mode" and its new endpoints such as `api/addresses/{address}/balance`.

ref: https://github.com/Alrighttt/walletd/tree/komodo-testnet-rebase

## Komodo DeFi Framework Draft Pull Request

The initial pull request with all Sia related changes thus far has been opened within the Komodo DeFi Framework github repository. This is a draft pull reques. It will be finalized and will be reviewed by the API team before being merged into the `dev` branch.

As of today, this pull request helps easily visualize all newly added Sia functionality to the DeFi Framework.

ref: https://github.com/KomodoPlatform/komodo-defi-framework/pull/2086

## Sia API Client Interface within DeFi Framework

The initial interface between the Komodo DeFi Framework API and Sia's walletd API has been established. This is currently only serves as an example on how to implement walletd API endpoints within the DeFi Framework.

Two endpoints have been integrated, `/api/consensus/tip` and `api/addresses/{address}/balance`.

ref: https://github.com/KomodoPlatform/komodo-defi-framework/blob/d180505b43f8167bd733263e73804ea60d4c1632/mm2src/coins/sia/http_client.rs#L102

## walletd API WASM Research

Some research was performed to assess the feasibility of using the WASM object produced by Sia's core/walletd within the DeFi Framework API.

The assessment is that it is not feasible to use this WASM object in any capacity. No further related work will be performed.

A bare bones example of how to build and utilize this WASM object was published.

ref: https://github.com/Alrighttt/sia-wasm-web-example

## Sia Rust

The beginnings of the Sia Rust library have been established. 

All functionality neccesary for generating addresses from arbitrary UnlockConditions or SpendPolicy objects has been established.

A series of unit tests have been established in both the Go and Rust codebases to easily identify any potential future discrepencies.

https://github.com/Alrighttt/core/commit/6c19657baf738c6b730625288e9b5413f77aa659

The tests found in the above "rust_port_test.go" will immediately identify any changes that must be incorporated into Sia Rust if the Sia developers change any fundamental data types or hashing or encoding functions for these data types.

## Next Steps

The testnet setup will be reorganized in the coming weeks as manual testing of the consensus mechanisms continue. The Komodo persistent testnet will be re-established in the coming weeks.

Further unit tests will be established within both the Go and Rust codebases as additional data types are ported to Sia Rust. The current goal is to port all data structures neccesary to create and serialize Sia transactions.

The draft pull request within the DeFi Framework will be finalized, reviewed and merged into the `dev` branch.

The initially planned "Sia Consensus Model Testing Report" will be delivered as the neccesary tooling is developed to produce Sia transactions from with the DeFi Framework. The SpendPolicy and UnlockConditions data structures being ported are a major step towards this.
