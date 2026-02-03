---
layout: default
title: Stability Pool & Liquidations
parent: English
nav_order: 3
---

# Stability Pool and Liquidations

### What is the Stability Pool?

The Stability Pool is the first line of defense in maintaining system solvency. It achieves that by acting as the source of liquidity to repay debt from [liquidated](stability-pool-and-liquidations.md#what-are-liquidations) Troves—ensuring that the total MEUR supply always remains backed.

When any [Trove](borrowing.md#what-is-a-trove) is liquidated, an amount of MEUR corresponding to the remaining debt of the Trove is burned from the Stability Pool's balance to repay its debt. In exchange, the **entire collateral** from the Trove is transferred to the Stability Pool.

The Stability Pool is funded by users transferring MEUR into it (called Stability Providers). Over time Stability Providers lose a pro-rata share of their MEUR deposits, while gaining a pro-rata share of the liquidated collateral. However, because Troves are likely to be liquidated at just below `110%` collateral ratios, it is expected that Stability Providers will receive a greater Euro-value of collateral relative to the debt they pay off.

### Why should I deposit MEUR to the Stability Pool?

Stability Providers will make liquidation gains ([see below](stability-pool-and-liquidations.md#how-do-i-benefit-as-a-stability-provider-from-liquidations)) and receive early adopter rewards in form of MSIC tokens.

### What are liquidations?

To ensure that the entire stablecoin supply remains fully backed by collateral, [Troves](borrowing.md#what-is-a-trove) that fall under the minimum collateral ratio of `110%` will be closed (liquidated).

The debt of the Trove is canceled and absorbed by the Stability Pool and its collateral distributed among Stability Providers.

The owner of the Trove still keeps the full amount of MEUR borrowed but loses `~10%` value overall hence it is critical to always keep the ratio above `110%`, ideally above `150%`.

### Who can liquidate Troves?

Anybody can liquidate a Trove as soon as it drops below the Minimum Collateral Ratio of `110%`. The initiator receives a gas compensation (`2 MEUR` + `0.5%` of the Trove's collateral) as reward for this service.

### How am I compensated for liquidating a Trove?

The liquidation of Troves is connected with certain gas costs which the initiator has to cover. The cost per Trove was reduced by implementing batch liquidations of up to 160 - 185 Troves but with the aim of ensuring that liquidations remain profitable even in times of soaring gas prices the protocol offers a gas compensation given by the following formula:

`gas compensation = 2 MEUR + 0.5% of Trove's collateral (REEF)`

The `2 MEUR` is funded by a [Liquidation Reserve](borrowing.md#what-is-the-liquidation-reserve) while the variable `0.5%` part (in REEF) comes from the liquidated collateral, slightly reducing the liquidation gain for Stability Providers.

### How do I benefit as a Stability Provider from liquidations?

As liquidations happen just below a collateral ratio of `110%`, you will most likely experience a net gain whenever a [Trove](borrowing.md#what-is-a-trove) is liquidated.

Let's say there is a total of `1,000,000 MEUR` in the Stability Pool and your deposit is `100,000 MEUR`.

Now, a Trove with debt of `200,000 MEUR` and collateral of `40,000,000 REEF` is liquidated at a REEF price of `€0.00545`, and thus at a collateral ratio of `109% (= 100% * (40,000,000 * 0.00545) / 200,000)`. Given that your pool share is `10%`, your deposit will go down by `10%` of the liquidated debt (`20,000 MEUR`), i.e. from `100,000` to `80,000 MEUR`. In return, you will gain `10%` of the liquidated collateral, i.e. `4,000,000 REEF`, which is currently worth `€21,800`. Your net gain from the liquidation is `€1,800`.

Note that depositors can immediately withdraw the collateral received from liquidations and sell it to reduce their exposure to REEF, if the Euro value of REEF is expected to decrease (for an exception see [Can I withdraw my deposit whenever I want?](stability-pool-and-liquidations.md#can-i-withdraw-my-deposit-whenever-i-want)).

### How do I benefit as a Stability Provider from early adopter rewards?

First you need to open a Trove, borrow MEUR, and deposit it to the Stability Pool. After making your deposit, you will start accumulating a reward (in MSIC) proportional to the size of your deposit on a continuous basis. Rewards will be the highest for early adopters of the system.

At any point in time, you can withdraw your pending rewards to your Reef Chain address.

### Can I withdraw my deposit whenever I want?

As a general rule, you can withdraw the deposit made to the Stability Pool at any time. There is no minimum lockup duration. However, withdrawals are temporarily suspended whenever there are liquidatable [Troves](borrowing.md#what-is-a-trove) with a collateral ratio below `110%` that have not been liquidated yet.

### What oracle are you using to determine the price of REEF?

The protocol uses a price oracle to determine the REEF:EUR price. Details about the specific oracle implementation will be provided when contracts are deployed.

### Can I lose money by depositing funds to the Stability Pool?

While liquidations will occur at a collateral ratio well above `100%` most of the time, it is theoretically possible that a [Trove](borrowing.md#what-is-a-trove) gets liquidated below `100%` in a flash crash or due to an oracle failure. In such a case, you may experience a loss since the collateral gain will be smaller than the reduction of your deposit.

If MEUR is trading above `€1`, liquidations may become unprofitable for Stability Providers even at collateral ratios higher than `100%`. However, this loss is hypothetical since MEUR is expected to return to the peg, so the "loss" only materializes if you had withdrawn your deposit and sold the MEUR at a price above `€1`.

Please note that although the system is diligently designed, a hack or a bug that results in losses for the users can never be fully excluded.

### What happens if the Stability Pool is empty when liquidations occur?

If the Stability Pool is empty, the system uses a secondary liquidation mechanism called redistribution. In such a case, the system redistributes the debt and collateral from liquidated Troves to all other existing Troves. The redistribution of debt and collateral is done in proportion to the recipient Trove's collateral amount.
