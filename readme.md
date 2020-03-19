# defi-oracles

> A curated list of oracle methods used in decentralized finance (DeFi) projects.


## Contents
- [Aave](#Aave)
- [Augur](#Augur)
- [bZx](#bZx)
- [Compound](#Compound)
- [DDEX](#DDEX)
- [dYdX](#dYdX)
- [MakerDAO](#MakerDAO)
- [Nexus Mutual](#Nexus-Mutual)
- [Nuo](#Nuo)
- [Synthetix](#Synthetix)
- [Token Sets](#Token-Sets)


## Aave
### Oracle Method
Aave uses separate Chainlink Price Reference Data contracts for each of the 15 price oracles needed to secure the accurate issuance and liquidation of cryptocurrency-backed loans. These data feeds are for assets priced against ETH and include LEND, LINK, BTC, MKR, MANA, KNC, USDC, REP, ZRX, BAT, DAI, TUSD, USDT, SUSD, and SNX.

Chainlink’s Price Reference Data Contracts are decentralized oracle networks made up of at least 7 independent, security reviewed, and Sybil resistant node operators. They derive from a growing pool of 30 independent node operators run by leading blockchain DevOps and security teams, many of which have extensive experience running POS nodes across multiple blockchain networks.

On-chain prices are calculated by having each independent node retrieve data from one of the numerous different market data aggregators, with every network containing at least seven independent data aggregator APIs. The nodes’ individual responses are then aggregated together on-chain into a collective response that becomes a new on-chain price update to the Price Reference Data Contract. Updates occur every 1% deviation in price (2% for less used assets), with a minimum time-based update every hour if the deviation threshold is not reached.

### Source
- https://medium.com/aave/the-aave-oracle-network-powered-by-chainlink-is-now-live-45bb8a5a8c4e
- https://feeds.chain.link

## Augur
### Oracle Method
After a market enters reporting, an Initial Reporter (typically the market creator), selects which outcome occurred. This becomes the “Tentative Winning Outcome.”

Users can dispute the Tentative Winning Outcome by staking REP on an alternative outcome that they believe to be correct. An alternative outcome requires a specified threshold of REP, which is called the Dispute Bond, to be staked on it in order to become the new Tentative Winning Outcome.

In v2, if you stake REP in favor of an outcome that the market ends up resolving to, you receive a 40% ROI on your staked REP (except in the case of an usued pre-stake or initial reporting). If you stake on an outcome that the market does not end up resolving to, you lose your entire stake.

With each successive dispute round, a higher Dispute Bond is needed to shift the Tentative Winning Outcome. A user may contribute the full Dispute Bond or fill it partially as part of a crowd-sourced fill along with other users.

### Source
- https://www.augur.net/blog/v2-resolution

## bZx
### Oracle Method
bZx uses separate Chainlink Price Reference Data contracts for each of the 6 price oracles (BTC/ETH, KNC/ETH, LINK/ETH, ZRX/ETH, DAI/ETH, and SUSD/ETH) needed to secure the accurate issuance and liquidation of loans for margin trading.

Chainlink’s Price Reference Data Contracts are decentralized oracle networks made up of at least 7 independent, security reviewed, and Sybil resistant node operators. They derive from a growing pool of 30 independent node operators run by leading blockchain DevOps and security teams, many of which have extensive experience running POS nodes across multiple blockchain networks.

On-chain prices are calculated by having each independent node retrieve data from one of the numerous different market data aggregators, with every network containing at least seven independent data aggregator APIs. The nodes’ individual responses are then aggregated together on-chain into a collective response that becomes a new on-chain price update to the Price Reference Data Contract. Updates occur every 1% deviation in price (2% for KNC/ETH and BTC/ETH), with a minimum time-based update every hour if the deviation threshold is not reached.

### Source
- https://bzx.network/blog/chainlink-oracles
- https://feeds.chain.link

## Compound
### Oracle Method
The price of BAT, REP, ZRX, and WBTC are a median of prices from Coinbase Pro, Bittrex, Poloniex, and Binance, denominated in Ether, and posted on-chain after a 1% deviation in an asset’s median price. For security, price changes are limited (at the protocol level) to 10% per hour, unless a manual approval is provided by a second, offline address. DAI, SAI, and USDC are based on Maker’s ETH/USD price feed.

Compound is developing an advanced price feed, the Open Oracle System, to create a transparent, decentralized, resilient, and tamper-proof price feed.

### Contract Addresses
- PriceOracle: [0x1d8aedc9e924730dd3f9641cdb4d1b92b848b4bd](https://etherscan.io/address/0x1d8aedc9e924730dd3f9641cdb4d1b92b848b4bd)

### Source
- https://medium.com/compound-finance/faq-1a2636713b69
- https://medium.com/compound-finance/announcing-compound-open-oracle-development-cff36f06aad3
- https://compound.finance/developers

## DDEX
### Oracle Method
Uses on-chain price oracles to determine real-time USD prices. These price oracles are different for each market (example: the ETH-DAI market will use the MakerDAO ETH-USD price oracle), chosen based on stability. They have several safety mechanisms built into the price determination process to guard against oracle failures: both on a contract level and algorithmically.

USDC references Coinbase prices, with safety checks, outlier detection, and expiration time built into their onchain proxy.

There are sanity bounds placed on the price of DAI, currently set to 0.95 and 1.05

### Contract Addresses
- DAI: [0xe6f148448b61339a59eF6aB9ab7378E9200FA745](https://etherscan.io/address/0xe6f148448b61339a59ef6ab9ab7378e9200fa745)

### Source
- https://medium.com/hydro-protocol/ddex-faq-margin-trading-bd4b32beb9f
- https://medium.com/ddex/reflecting-on-ddex-in-the-age-of-flash-loans-ee55410e0974
- https://samczsun.com/taking-undercollateralized-loans-for-fun-and-for-profit

## dYdX
### Oracle Method
Prices are fed to the dYdX smart contracts through price oracles that run on Ethereum. dYdX uses different price oracles for different assets.

For ETH, dYdX uses the MakerDAO ETH-USD V1 Oracle that is used by MakerDAO for their stablecoin SAI, and relies on a distributed network of reporters that report the price of ETH in USD.

For SAI, dYdX uses a price of $1. SAI can no longer be borrowed and is basically worth 0 as collateral. We only include this oracle method for completeness.

For DAI, dYdX uses our own price oracle which calculates the USD price of DAI using a combination of Oasis Trade's on-chain orderbook, Uniswap, and the MakerDAO ETH-USD oracle. The oracle also has several protections against price manipulation on eth2dai and Uniswap.

For USDC, dYdX uses a price of $1 as USDC is exchangeable 1:1 with USD on Coinbase.

### Contract Addresses
Up-to-date contract addresses for the Oracles that dYdX uses can be obtained by calling the `getMarketPriceOracle` function on [dYdX's Solo Margin contract](https://etherscan.io/address/0x1e0447b19bb6ecfdae1e4ae1694b0c3659614e4e).

Currently the addresses are:

- WETH Oracle (Market ID 0): [0xf61AE328463CD997C7b58e7045CdC613e1cFdb69](https://etherscan.io/address/0xf61AE328463CD997C7b58e7045CdC613e1cFdb69)
- SAI Oracle (Market ID 1): [0x91d8825e0294d6628f8C93ac8ddA88773618608a](https://etherscan.io/address/0x91d8825e0294d6628f8c93ac8dda88773618608a)
- USDC Oracle (Market ID 2): [0x52f1c952A48a4588f9ae615d38cfdbf8dF036e60](https://etherscan.io/address/0x52f1c952A48a4588f9ae615d38cfdbf8dF036e60)
- DAI Oracle (Market ID 3): [0x0fBd14718d8FAB8f9f40Ee5c5612b1F0717100A2](https://etherscan.io/address/0x0fbd14718d8fab8f9f40ee5c5612b1f0717100a2)

### Source
- https://help.dydx.exchange/en/articles/2953486-where-does-price-information-come-from
- https://docs.dydx.exchange/#/contracts

## MakerDAO
### Oracle Method
The reference price (ETHUSD) for the Maker system is provided via an oracle (the medianizer), which collates price data from a number of external price feeds.

Independent price feed operators constantly monitor the reference price across a number of external sources and will submit updates to the blockchain when:

1. Source price differs to the most recently submitted price by more than the defined amount (currently 1%)
2. Last price update was more than 6 hours ago.

Price updates are written to the blockchain via price feed contracts which are deployed and owned by feed operators. Price feed contracts which have been whitelisted by the medianizer are able to forward their prices for inclusion in the medianized price.

The medianizer is the smart contract which provides Makers trusted reference price.

It maintains a whitelist of price feed contracts which are allowed to post price updates and a record of recent prices supplied by each address. Every time a new price update is received the median of all feed prices is re-computed and the medianized value is updated.

Permissions:

The adding and removal of whitelisted price feed addresses is controlled via governance, as is the setting of the min parameter - the minimum number of valid feeds required in order for the medianized value to be considered valid.

v2 introduces several new proposals:
1. Add a set of DeFi partners as Feeds
2. An Oracle Team Mandate to create an Oracle Team role. The mandate will empower MKR Governance to appoint Oracle Team(s) to perform certain tasks on their behalf.
3. MKR Governors’ control of the Oracles infrastructure be formalized via an Oracle Governance Framework.
4. New incentive structure for Oracles.

### Contract Addresses
- Maker: [0x99041F808D598B782D5a3e498681C2452A31da08](https://etherscan.io/address/0x99041F808D598B782D5a3e498681C2452A31da08)
- Ethereum: [0x81FE72B5A8d1A857d176C3E7d5Bd2679A9B85763](https://etherscan.io/address/0x81FE72B5A8d1A857d176C3E7d5Bd2679A9B85763)
- Basic Attention Token: [0xB4eb54AF9Cc7882DF0121d26c5b97E802915ABe6](https://etherscan.io/address/0xB4eb54AF9Cc7882DF0121d26c5b97E802915ABe6)

### Source
- https://developer.makerdao.com/feeds
- https://blog.makerdao.com/introducing-oracles-v2-and-defi-feeds

## Nexus Mutual
### Oracle Method
Members will act as judges, with each claim subject to a yes/no vote by members who have chosen to stake a portion of their tokens to act as Claims Assessors.
The Claims Assessors earn rewards for voting with the consensus outcome. If anyone is deemed to have voted fraudulently, their stake may be burned via the Governance process.

Nexus Mutual is using Chainlink’s price reference data contracts for valuations of the multi-currency capital pool. Nexual Mutual performs daily on-chain updates and rebalances of its minimum capital requirement (MCR) by consistently recalculating the value of each capital asset (currently ETH and DAI) in the multi-currency pool using Chainlink’s Price Reference Data Contracts.

### Source
- https://nexusmutual.gitbook.io/docs/faq
- https://medium.com/nexus-mutual/nexus-mutual-is-now-using-chainlinks-price-reference-data-contracts-for-decentralized-valuations-6a62c5d4e030

## Nuo
### Oracle Method
For any currency pair, Nuo uses best price provided by decentralised exchanges (Pd) and hard-fences it using volume weighted average price aggregated over price feeds from centralised exchanges (Pc).

Currently Nuo uses Kyber and Uniswap as decentralised partner exchanges. Among centralised exchanges, Nuo tracks price and volume across all major cexes with >50 total cexes added already.

At any time, for any currency pair,
Pd = Best Price across partner decentralised exchanges
Pc = TimeDecaySum( Sum( VolumeOfCex * PriceByCex ) / TotalVolumeAcrossAllCexes )

VolumeOfCex, PriceByCex and TotalVolumeAcrossAllCexes use clustering techniques to remove anomalies in price/volume and ignore exchanges with poor pricing.

TimeDecaySum is built to reduce effect of a high volume exchange going offline for a while by reducing the weight of the price obtained from a cex based on the duration when the last trade was recorded from it.

For any currency pair, Nuo hard-fencing ensures the following holds true:
lower_fence * Pc < Pd < upper_fence * Pc

Currently, fencing percentage is placed at 10% system-wide. Hence, lower_fence = 0.9 and upper_fence = 1.1. We can expect a tighter fence as dexes get more efficient and liquid in future

At any point in time, if the above condition does not hold true, the exchange market is paused and resumed again when the condition becomes true. This is done to prevent any unwanted liquidations from happening on the platform due to price manipulations or flash crashes across our partner dexes.

There are plans to potentially integrate Chainlink in a future version.

### Source
- https://nuo.drift.help/article/how-does-nuo's-price-feed-work
- https://twitter.com/getnuo/status/1230221716934340608

## Synthetix
### Oracle Method
Chainlink for FX and commodity price feeds with plan to integrate cryptocurrencies and indices in the future.

Other price feeds are determined by an oracle that pushes price feeds on-chain using an algorithm with a variety of sources to form an aggregate value for each asset.

The ExchangeRates contract (https://contracts.synthetix.io/ExchangeRates) will continue to be fed prices from the decentralized oracle. However, the logic for looking up prices will be extended with a mapping of Chainlink Aggregator contracts for each Synth.

### Contract Addresses
- ExchangeRates: [0x9D7F70AF5DF5D5CC79780032d47a34615D1F1d77](https://etherscan.io/address/0x9D7F70AF5DF5D5CC79780032d47a34615D1F1d77)

### Source
- https://blog.synthetix.io/chainlink-decentralizes-first-wave-of-synthetix-price-feeds
- https://www.synthetix.io/uploads/synthetix_litepaper.pdf
- https://sips.synthetix.io/sips/sip-36
- https://sips.synthetix.io/sips/sip-32

## Token Sets
### Oracle Method
On-chain prices used by their smart contracts are sourced from MakerDAO's oracles (BTC and ETH), and prices for buying and selling are sourced from DEXs that provide liquidity to Set Protocol. They use Chainlink's LINK/USD oracle to power the LINK sets and also have their own on-chain moving average and RSI oracles.

Each Smart Contract Managed Rebalancing Set system is made of three distinct parts: 1) Manager Contract that generates rebalancing proposals based off on-chain data, 2) Oracles that are used to provide data to the Manager Contract and, 3) the Rebalancing Set Token that stores state (balances, allocations, etc.) regarding the strategy.

Currently, HistoricalPriceFeeds use data from Maker’s oracles to build a price history for the underlying asset, but any oracle adhering to Maker's interface could be used. The HistoricalPriceFeed is intended to represent the historical prices of one asset at consistent time intervals. Additionally, there is a defined upper limit to the amount of historical data, after which old data is overwritten.

The MovingAverageOracle leverages data available from the HistoricalPriceFeed to calculate a simple moving average of a desired amount of data points.


### Contract Addresses
- HistoricalPriceFeed: [0x7956cE4fbA992987A11bd44ff0Ddb62504711Be8](https://etherscan.io/address/0x7956cE4fbA992987A11bd44ff0Ddb62504711Be8)
- HistoricalPriceFeed medianizerAddress: [0x729D19f657BD0614b4985Cf1D82531c67569197B](https://etherscan.io/address/0x729D19f657BD0614b4985Cf1D82531c67569197B)
- MovingAverageOracle: [0x90b242eDd278E636E02C2054C861Fd46A7B96271](https://etherscan.io/address/0x90b242eDd278E636E02C2054C861Fd46A7B96271)
- HistoricalPriceFeed priceFeedAddress: [0x7956cE4fbA992987A11bd44ff0Ddb62504711Be8](https://etherscan.io/address/0x7956cE4fbA992987A11bd44ff0Ddb62504711Be8)

### Source
- https://www.tokensets.com
- https://medium.com/set-protocol/introducing-the-link-rsi-set-on-tokensets-fe3b4fcacf94
- https://github.com/SetProtocol/set-protocol-strategies/wiki

## Additional Resources

- [What are Oracles?](https://docs.ethhub.io/built-on-ethereum/oracles/what-are-oracles/) by EthHub
- [What is an oracle? How smart contracts see the world](https://defipulse.com/blog/what-is-an-oracle-how-smart-contracts-see-the-world/) by DeFi Pulse
- [Decentralised Oracles: a comprehensive overview](https://medium.com/fabric-ventures/decentralised-oracles-a-comprehensive-overview-d3168b9a8841)


## Contribute

Contributions welcome! Read the [contribution guidelines](contributing.md) first.


## License

[![CC0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, Linda Xie has waived all copyright and
related or neighboring rights to this work.
