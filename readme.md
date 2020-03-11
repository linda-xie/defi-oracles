# defi-oracles

> A curated list of oracle methods used in decentralized finance (DeFi) projects.


## Contents
- [Aave](#Aave)
- [Augur](#Augur)


## Aave
**Oracle Method**:
Chainlink for 16 cryptocurrency price feeds

**Source**:
https://medium.com/aave/the-aave-oracle-network-powered-by-chainlink-is-now-live-45bb8a5a8c4e

## Augur
**Oracle Method**:
After a market enters reporting, an Initial Reporter (typically the market creator), selects which outcome occurred. This becomes the “Tentative Winning Outcome.”

Users can dispute the Tentative Winning Outcome by staking REP on an alternative outcome that they believe to be correct. An alternative outcome requires a specified threshold of REP, which is called the Dispute Bond, to be staked on it in order to become the new Tentative Winning Outcome.

In v2, if you stake REP in favor of an outcome that the market ends up resolving to, you receive a 40% ROI on your staked REP (except in the case of an usued pre-stake or initial reporting). If you stake on an outcome that the market does not end up resolving to, you lose your entire stake.

With each successive dispute round, a higher Dispute Bond is needed to shift the Tentative Winning Outcome. A user may contribute the full Dispute Bond or fill it partially as part of a crowd-sourced fill along with other users.

**Source**:
https://www.augur.net/blog/v2-resolution/

## Contribute

Contributions welcome! Read the [contribution guidelines](contributing.md) first.


## License

[![CC0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, Linda Xie has waived all copyright and
related or neighboring rights to this work.
