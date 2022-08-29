---
sidebar_position: 2
title: Subgraph Entities
---

# Entities

- [`Balancer`](#balancer)
- [`Pool`](#pool)
- [`PoolToken`](#pooltoken)
- [`PriceRateProvider`](#pricerateprovider)
- [`PoolShare`](#poolshare)
- [`User`](#user)
- [`UserInternalBalance`](#userinternalbalance)
- [`GradualWeightUpdate`](#gradualweightupdate)
- [`AmpUpdate`](#ampupdate)
- [`Swap`](#swap)
- [`JoinExit`](#joinexit)
- [`LatestPrice`](#latestprice)
- [`PoolHistoricalLiquidity`](#poolhistoricalliquidity)
- [`TokenPrice`](#tokenprice)
- [`ManagementOperation`](#managementoperation)
- [`PoolSnapShot`](#poolsnapshot)
- [`Token`](#token)
- [`TokenSnapShot`](#tokensnapshot)
- [`TradePair`](#tradepair)
- [`TradePairSnapshot`](#tradepairsnapshot)
- [`BalancerSnapshot`](#balancersnapshot)

# Balancer

Description: General information about Balancer Pools

| Field           | Type             | Description                    |
| --------------- | ---------------- | ------------------------------ |
| id              | ID!              |                                |
| poolCount       | Int!             | how many pools                 |
| pools           | [`Pool!`](#pool) | choose which pool              |
| totalLiquidity  | BigDecimal!      | how much liquidity pool has    |
| totalSwapCount  | BigInt!          | quantity of swaps              |
| totalSwapVolume | BigDecimal!      | how much value has been swaped |
| totalSwapFee    | BigDecimal!      | how much fees collected        |

# Pool

Description: various information about balancer pools

| Field                   | Type                                                  | Description                 |
| ----------------------- | ----------------------------------------------------- | --------------------------- |
| id                      | ID!                                                   |                             |
| address                 | Bytes!                                                | address of user             |
| poolType                | String                                                | which type of balancer pool |
| factory                 | Bytes                                                 |                             |
| strategyType            | Int!                                                  |                             |
| oracleEnabled           | Boolean!                                              |                             |
| symbol                  | String                                                |                             |
| name                    | String                                                |                             |
| swapEnabled             | Boolean!                                              |                             |
| swapFee                 | BigDecimal!                                           |                             |
| owner                   | Bytes                                                 |                             |
| totalWeight             | BigDecimal                                            |                             |
| totalSwapVolume         | BigDecimal!                                           |                             |
| totalSwapFee            | BigDecimal!                                           |                             |
| totalLiquidity          | BigDecimal!                                           |                             |
| totalShares             | BigDecimal!                                           |                             |
| createTime              | Int!                                                  |                             |
| swapCount               | BigInt!                                               |                             |
| holdersCount            | BigInt!                                               |                             |
| vaultID                 | Balancer!                                             |                             |
| tx                      | Bytes                                                 |                             |
| tokensList              | [Bytes!]!                                             |                             |
| tokens                  | [`PoolToken!`](#pooltoken)                            |                             |
| swaps                   | [`Swap!`](#swap)                                      |                             |
| shares                  | [`PoolShare!`](#poolshare)                            |                             |
| snapshots               | [`PoolSnapShot!`](#poolsnapshot)                      |                             |
| historicalValues        | [`PoolHistoricalLiquidity!`](#poolhistoricaliquidity) |                             |
| weightUpdates [^1]      | [`GradualWeightUpdate!`](#gradualweightupdate)        |                             |
| amp [^2]                | BigInt                                                |
| priceRateProviders [^3] | [`PriceRateProvider`](#pricerateprovider)             |                             |
| principalToken [^4]     | Bytes                                                 |                             |
| baseToken [^4]          | Bytes                                                 |                             |
| expirtyTime [^4]        | BigInt                                                |                             |
| unitSeconds [^4]        | BigInt                                                |                             |
| managementFee [^5]      | BigDecimal                                            |                             |
| mainIndex [^6]          | Int                                                   |                             |
| wrappedIndex [^6]       | Int                                                   |                             |
| lowerTarget [^6]        | BigDecimal                                            |                             |
| upperTarget [^6]        | BigDecimal                                            |                             |
| sqrtAlpha [^7]          | BigDecimal                                            |                             |
| sqrtBeta [^7]           | BigDecimal                                            |                             |
| root3Alpha [^8]         | BigDecimal                                            |                             |

[^1]: Liquiditybootstrappingpoolonly
[^2]: Stablepoolonly
[^3]: MetastablepoolandLinearPoolOnly
[^4]: ConvergentCurvePoolElementOnly
[^5]: InvestmentPoolOnly
[^6]: LinearPoolONly
[^7]: Gyro2PoolOnly
[^8]: Gyro3PoolOnly

# PoolToken

Description: list of tokens wihtin balancer pools

| Field         | Type                   | Description                       |
| ------------- | ---------------------- | --------------------------------- |
| id            | ID!                    |                                   |
| poolId        | Pool                   | a unigue identifier for each pool |
| token         | Token!                 |                                   |
| assetManager  | Bytes                  |                                   |
| symbol        | String!                | pool token symbol                 |
| decimals      | Int!                   |                                   |
| address       | String!                |                                   |
| priceRate     | BigDecimal!            | conversion of token swapped       |
| balance       | BigDecimal!            | token balance of pool token       |
| cashBalance   | BigDecimal!            | cash balance of pool token        |
| manageBalance | BigDecimal!            |                                   |
| management    | [ManagementOperation!] |                                   |
| weight [^9]   | BigDecimal             |                                   |

[^9]: weightedpoolonly

# PriceRateProvider

Description: provides information of swaps

| Field          | Type        | Description                       |
| -------------- | ----------- | --------------------------------- |
| id             | ID!         |                                   |
| poolID         | Pool!       | a unigue identifier for each pool |
| token          | PoolToken!  |                                   |
| address        | Bytes!      |                                   |
| rate           | BigDecimal! |                                   |
| lastCached     | Int!        |                                   |
| cachedDuration | Int!        | how long estimate rate will last  |
| cashExpiry     | Int!        |                                   |

# PoolShare

Description: information of shares users have

| Field       | Type        | Description                       |
| ----------- | ----------- | --------------------------------- |
| id          | ID!         |                                   |
| userAddress | User!       | user wallet address               |
| poolId      | Pool!       | a unigue identifier for each pool |
| balance     | BigDecimal! | balance of pool                   |

# User

Description: information of balancer users

| Field                | Type                                           | Description               |
| -------------------- | ---------------------------------------------- | ------------------------- |
| id                   | ID!                                            |                           |
| sharesOwned          | [`PoolShare!`](#poolshare)                     | how many shares user owns |
| swaps                | [`Swap!`](#swap)                               |                           |
| userInternalBalances | [`UserInternalBalance!`](#userinternalbalance) |                           |

# UserInternalBalance

Description: check balance of each token

| Field       | Type        | Description               |
| ----------- | ----------- | ------------------------- |
| id          | ID!         |                           |
| userAddress | User        | wallet address            |
| token       | Bytes!      | token checking balance on |
| balance     | BigDecimal! | balance of token          |

# GradualWeightUpdate

Description: information of when pools change token percentage

| Field              | Type    | Description                       |
| ------------------ | ------- | --------------------------------- |
| id                 | ID!     |                                   |
| poolId             | Pool!   | a unigue identifier for each pool |
| scheduledTimestamp | Int!    |                                   |
| startTimestamp     | BigInt! |                                   |
| endTimestamp       | BigInt! |                                   |
| startWeights       | BigInt! |                                   |
| endWeights         | BigInt! |                                   |

# AmpUpdate

Description: Unsure?

| Field              | Type    | Description                       |
| ------------------ | ------- | --------------------------------- |
| id                 | ID!     |                                   |
| poolId             | Pool!   | a unigue identifier for each pool |
| scheduledTimestamp | Int!    |                                   |
| startTimestamp     | BigInt! | Start time                        |
| endTimestamp       | BigInt! | end time                          |
| startAmp           | BigInt! |                                   |
| endAmp             | BigInt! |                                   |

# Swap

Description: information about users swaps

| Field          | Type        | Description                       |
| -------------- | ----------- | --------------------------------- |
| id             | ID!         |                                   |
| caller         | Bytes!      |                                   |
| tokenIn        | Bytes!      | which token swapped in            |
| tokenInSym     | String!     | symbol of token swapped in        |
| tokenOut       | Bytes!      | which token swapped out           |
| tokenOutSym    | String!     | symbol of token swapped out       |
| tokenAmountIn  | BigDecimal! | amount of token swapped           |
| tokenAmountOut | BigDecimal! | amount of tokens received         |
| valueUSD       | BigDecimal! | value in USD                      |
| poolId         | Pool!       | a unigue identifier for each pool |
| userAddress    | User!       | user wallet address               |
| timestamp      | Int!        | time stamp of when swap occured   |
| tx             | Bytes!      | fee for swap                      |

# JoinExit

Description: info when user joins or exits pool

| Field     | Type           | Description                |
| --------- | -------------- | -------------------------- |
| id        | ID!            |                            |
| type      | InvestType!    |                            |
| sender    | Bytes!         |                            |
| amounts   | [BigDecimal!]! |                            |
| pool      | Pool!          |                            |
| user      | User!          |                            |
| timestamp | Int!           | time stamp of join or exit |
| tx        | Bytes!         | fee paid                   |

# LatestPrice

Description: check lates token price

| Field        | Type        | Description                         |
| ------------ | ----------- | ----------------------------------- |
| id           | ID!         |                                     |
| asset        | Bytes!      |                                     |
| pricingAsset | Bytes!      | address of stable asset             |
| poolID       | Pool!       | last pool which set price           |
| price        | BigDecimal! | all the latest prices               |
| block        | BigInt!     | last block that prices were updated |

# PoolHistoricalLiquidity

Description: Historical liquidity of pools

| Field           | Type        | Description                                      |
| --------------- | ----------- | ------------------------------------------------ |
| id              | ID!         |                                                  |
| poolId          | Pool!       | a unigue identifier for each pool                |
| poolTotalShares | BigDecimal! | total pool shares                                |
| poolLiquidity   | BigDecimal! | total value, priced in the stable asset - ie USD |
| poolShareValue  | BigDecimal! | total pool value                                 |
| pricingAsset    | Bytes!      | address of stable asset                          |
| block           | BigInt!     | last block that prices were updated              |

# TokenPrice

Description: checking price of tokens

| Field        | Type        | Description                                     |
| ------------ | ----------- | ----------------------------------------------- |
| id           | ID!         | address of token + address of stablecoin-poolId |
| poolId       | Pool!       | a unigue identifier for each pool               |
| asset        | Bytes!      | list of assets                                  |
| amount       | BigDecimal! | amount of token                                 |
| pricingAsset | Bytes!      | address of stable asset                         |
| price        | BigDecimal! | price of token                                  |
| block        | BigInt!     | last block that prices were updated             |
| timestamp    | Int!        | time price is checked                           |

# ManagementOperation

Description: Unsure?

| Field       | Type           | Description                       |
| ----------- | -------------- | --------------------------------- |
| id          | ID!            |                                   |
| type        | OperationType! |                                   |
| cashDelta   | BigDecimal!    |                                   |
| manageDelta | BigDecimal!    |                                   |
| poolTokenID | PoolToken!     | a unigue identifier for each pool |
| timestamp   | Int!           | timestamp operation occurs        |

# PoolSnapshot

Description: a "snapshot" of the Ethereum blockchain for each pool at a certain block number before voting opens.

| Field       | Type           | Description                         |
| ----------- | -------------- | ----------------------------------- |
| id          | ID!            |                                     |
| pool        | Pool!          | name of pools included              |
| amounts     | [BigDecimal!]! | amount of pools included            |
| totalShares | BigDecimal!    | total shares of pool before vote    |
| swapVolume  | BigDecimal!    | total volume of pool before vote    |
| swapFees    | BigDecimal!    | swap fee of pool before vote        |
| liquidity   | BigDecimal!    | total liquidity of pool before vote |
| timestamp   | Int!           | time snapshot occurs                |

# Token

Description: information of tokens within balancer

| Field                | Type        | Description                                                       |
| -------------------- | ----------- | ----------------------------------------------------------------- |
| id                   | ID!         | eth address of user                                               |
| symbol               | String      | symbol of token                                                   |
| name                 | String      | name of token                                                     |
| decimals             | Int!        |                                                                   |
| address              | String!     | token address                                                     |
| totalBalanceUSD      | BigDecimal! | total balance of tokens across balancer                           |
| totalBalanceNotional | BigDecimal! | total unrealized balance                                          |
| totalVolumeUSD       | BigDecimal! | total volume in fiat (usd)                                        |
| totalVolumeNotional  | BigDecimal! | total unrealized volume                                           |
| totalSwapCount       | BigInt!     | total swap count for token                                        |
| latestPrice          | LatestPrice | latest price of token, updated when pool liquidity changes        |
| latestUSDPrice       | BigDecimal! | latest price of token in USD, updated when pool liquidity changes |
| pool                 | Pool        | pool entity associated with the token, if it is a Balancer pool   |

# TokenSnapshot

Description: a "snapshot" of the Ethereum blockchain for each token at a certain block number before voting opens.

| Field                | Type        | Description                                      |
| -------------------- | ----------- | ------------------------------------------------ |
| id                   | ID!         | token address + dayId                            |
| token                | Token!      | which token or crypto                            |
| totalBalanceUSD      | BigDecimal! | total balance of tokens across balancer          |
| totalBalanceNotional | BigDecimal! | underlying asset balance                         |
| totalVolumeUSD       | BigDecimal! | amount of volume the token has moved on this day |
| totalVolumeNotional  | BigDecimal! | underyling asset volume                          |
| totalSwapCount       | BigInt!     | total swap count accross balancer                |

# TradePair

Description: information of trading pairs in balancer

| Field           | Type        | Description                   |
| --------------- | ----------- | ----------------------------- |
| id              | ID!         | Token Address - Token Address |
| token0          | Token!      | Token 1 of trading pair       |
| token1          | Token!      | Token 2 of trading part       |
| totalSwapVolume | BigDecimal! | Total swap volume of pair     |
| totalSwapFee    | BigDecimal! | Total swap fees of pair       |

# TradePairSnapshot

Description: a "snapshot" of the Ethereum blockchain of the trading pair at a certain block number before voting opens.

| Field           | Type        | Description                         |
| --------------- | ----------- | ----------------------------------- |
| id              | ID!         | user eth address                    |
| pair            | TradePair!  | trading pair used in vote           |
| timestamp       | Int!        | time snapshot took place            |
| totalSwapVolume | BigDecimal! | total volume at time of snapshot    |
| totalSwapFee    | BigDecimal! | total swap fees at time of snapshot |

# BalancerSnapshot

Description: a "snapshot" of the Ethereum blockchain at a certain block number before voting opens.

| Field           | Type        | Description                        |
| --------------- | ----------- | ---------------------------------- |
| id              | ID!         | User eth address                   |
| vault           | Balancer!   | which vault is associated to vote  |
| timestamp       | Int!        | time snapshot took place           |
| poolCount       | Int!        | how many pools in vote             |
| totalLiquidity  | BigDecimal! | total liquidity of pools in vote   |
| totalSwapCount  | BigInt!     | total swapcount of pools in vote   |
| totalSwapVolume | BigDecimal! | total swap volome of pools in vote |
| totalSwapFee    | BigDecimal! | total swap fees of pools in vote   |