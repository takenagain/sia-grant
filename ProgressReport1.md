# Progress Report #1

## Sia Skeleton Protocol

A minimal implementation of the Sia protocol was pushed to the sia-dev branch of https://github.com/komodoplatform/komodo-defi-framework 

This represents the foundation for the Sia protocol within the Komodo DeFi Framework and serves as a template for all future Sia related work.

This enables the integration of a Sia-based coin within the Komodo DeFi Framework API via the newly created `task::enable_sia::init` API endpoint.

Usage:

Start the Defi Framework API with the following within `coins` file:
```shell
  {
    "coin": "TSIA",
    "asset": "TSIA",
    "fname": "TSIA",
    "rpcport": 59842,
    "mm2": 0,
    "protocol": {
      "type": "SIA",
      "protocol_data": {
      }
    }
  }
```

Send a `POST` request with the following body:
```shell
{
	"userpass": "{{userpass}}",
    "mmrpc": "2.0",
    "method": "task::enable_sia::init",
    "params": {
        "ticker": "TSIA",
        "activation_params": {"http_url" : "http://localhost:9980/", "http_auth": "password"}
    }
}
```

This enables further commands such as `my_balance`. All endpoints currently provide mocked data or intentionally cause a thread to crash via the unimplemented!() Rust macro.

The relevant code for this "skeleton implementation" can be viewed in this git comparsion: https://github.com/KomodoPlatform/komodo-defi-framework/compare/af571608c34f38d82e3c421f9bd61c5265db0cf8...KomodoPlatform:komodo-defi-framework:sia-dev?expand=1

## Docker Testnet Framework

The basis for the Docker unit test framework has also been established within the Komodo DeFi Framework. This is based on the Dockerfile provided by the Sia team within the walletd repo. It has been adapted to establish a "komodo" testnet instead of the anagami testnet. 

The foundation address of this testnet has been changed to one controlled by the Komodo API team. This testnet has its POW difficulty lowered to allow blocks to be created on demand. 

Moving forward, another testnet will be established in a similar fashion. One testnet will work as a persistent internal testnet for the Komodo API team. The other testnet implementation will facilitate unit tests within the Komodo DeFi Framework and will not be persistent.

The relevant code can be found within this commit: https://github.com/KomodoPlatform/komodo-defi-framework/commit/32fdb85d74dd7f66466f6e1cae0ba53d367ab844

Usage:
```shell
cargo test --features "run-docker-tests" --package mm2_main --test docker_tests_main docker_tests::dummy -- --exact
```

## Walletd CPU miner changes

The need to create an arbitrary number of blocks with the walletd CPU miner was identified. A new parameter, `blocks`, was added to the `mine` command of walletd. This new parameter allows the user to specify how many blocks the CPU miner should mine before exiting. This is crucial for future unit tests within the Komodo DeFi Framework. 

A pull request adding this parameter was opened: https://github.com/SiaFoundation/walletd/pull/53

## Walletd /util/generateaddress Endpoint

A new walletd endpoint has been created to enable address generation from an arbitrary SpendPolicy. This was identified as a necessary first step towards testing the newly introduced consensus mechanisms that will allow for HLTC-like consensus mechanisms. 

The code is simple and relies on already established mechanisms for serializing and deserailizing the Go types within walletd. This endpoint is unlikely to be merged upstream or be made available to users unless requested. 

The code for this endpoint can be found in this commit: https://github.com/SiaFoundation/walletd/commit/0b53f40a281c6561b9beb3868f51a5feb8431c79

Usage:
```shell
curl -u :password --location 'http://localhost:9980/api/utils/generateaddress/' \
--header 'Content-Type: text/plain' \
--data '"thresh(1,[thresh(2,[after(1708697003),pk(0x0102030000000000000000000000000000000000000000000000000000000000)]),thresh(2,[h(0x0102030000000000000000000000000000000000000000000000000000000000),pk(0x0405060000000000000000000000000000000000000000000000000000000000)])])"'
```

## Next Steps

The Komodo API team will commence with manual testing of the newly introduced Sia consensus mechanisms.

ed25519 signature creation within the Komodo DeFi Framework has been identified as a useful first step in regards to this testing. Given arbitrary ed25519 signing using the DeFi Framework's private key handler, the API team can begin to produce complex HLTC transactions within walletd. 

As this consensus testing goes forward, various endpoints will be added to both the Komodo DeFi Framework and walletd APIs.

The interface between both APIs will be established as needed in order to facilitate this manual testing.

Unit tests utilizing the newly established walletd Docker framework within the Komodo DeFi Framework will be established in tandem with any new code for the Sia protocol integration.
