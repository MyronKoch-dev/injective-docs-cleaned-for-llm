# Oracle

## Abstract

This specification specifies the oracle module, which is primarily used by the `exchange` modules to obtain external price data.

## Workflow

1. New price feed providers must first obtain oracle privileges through a governance proposal, which grants privileges to a list of relayers. The exception to this is for the Coinbase price oracle, as anyone can send Coinbase price updates since they are already exclusively signed by the Coinbase oracle private key.\
   **Example Grant Proposals**: `GrantBandOraclePrivilegeProposal`, `GrantPriceFeederPrivilegeProposal`
2. Once the governance proposal is approved, the specified relayers can publish oracle data by sending relay messages specific to their oracle type.\
   **Example Relay Messages**:`MsgRelayBandRates`, `MsgRelayPriceFeedPrice`, `MsgRelayCoinbaseMessages` etc.
3. Upon receiving the relay message, the oracle module checks if the relayer account has grant privileges and persists the latest price data in the state.
4. Other Cosmos-SDK modules can then fetch the latest price data for a specific provider by querying the oracle module.

**Note**: In case of any discrepancy, the price feed privileges can be revoked through governance\
**Example Revoke Proposals**: `RevokeBandOraclePrivilegeProposal`, `RevokePriceFeederPrivilegeProposal` etc

## Band IBC integration flow

Cosmos SDK blockchains are able to interact with each other using IBC and Injective support the feature to fetch price feed from BandChain via IBC.

1. To communicate with BandChain's oracle using IBC, Injective Chain must first initialize a communication channel with the oracle module on the BandChain using relayers.
2. Once the connection has been established, a pair of channel identifiers is generated -- one for the Injective Chain and one for Band. The channel identifier is used by Injective Chain to route outgoing oracle request packets to Band. Similarly, Band's oracle module uses the channel identifier when sending back the oracle response.
3. To enable band IBC integration after setting up communication channel, the governance proposal for `EnableBandIBCProposal` should pass.
4. And then, the list of prices to be fetched via IBC should be determined by `AuthorizeBandOracleRequestProposal` and `UpdateBandOracleRequestProposal`.
5. Once BandIBC is enabled, chain periodically sends price request IBC packets (`OracleRequestPacketData`) to bandchain and bandchain responds with the price via IBC packet (`OracleResponsePacketData`). Band chain is providing prices when there are threshold number of data providers confirm, and it takes time to get the price after sending requests. To request price before the configured interval, any user can broadcast a `MsgRequestBandIBCRates` message, which is instantly executed.

## Contents

1. [**State**](https://github.com/InjectiveLabs/injective-docs/blob/gitbook/.gitbook/developers/modules/injective/oracle/01\_state.md)
2. [**Keeper**](https://github.com/InjectiveLabs/injective-docs/blob/gitbook/.gitbook/developers/modules/injective/oracle/02\_keeper.md)
3. [**Messages**](https://github.com/InjectiveLabs/injective-docs/blob/gitbook/.gitbook/developers/modules/injective/oracle/03\_messages.md)
4. [**Proposals**](https://github.com/InjectiveLabs/injective-docs/blob/gitbook/.gitbook/developers/modules/injective/oracle/04\_proposals.md)
5. [**Events**](https://github.com/InjectiveLabs/injective-docs/blob/gitbook/.gitbook/developers/modules/injective/oracle/05\_events.md)