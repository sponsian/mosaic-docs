---
layout: default
title: Redemptions & MEUR Stability
parent: English
nav_order: 4
---

# Redemptions and MEUR Price Stability

### How does MEUR closely follow the price of EUR?

The ability to redeem MEUR for REEF at face value (i.e. 1 MEUR for €1 of REEF) and the minimum collateral ratio of `110%` create a price floor and price ceiling (respectively) through arbitrage opportunities. We call these "hard peg mechanisms" since they are based on direct processes.

MEUR also benefits from less direct mechanisms for EUR parity — called "soft peg mechanisms". One of these mechanisms is parity as a Schelling point. Since Mosaic treats MEUR as being equal to EUR, parity between the two is an implied equilibrium state of the protocol. Another of these mechanisms is the borrowing fee on new debts. As redemptions increase (implying MEUR is below €1), so too does the `baseRate` — making borrowing less attractive which keeps new MEUR from hitting the market and driving the price below €1.

### What are redemptions?

A redemption is the process of exchanging MEUR for REEF at face value, as if 1 MEUR is exactly worth €1. That is, for x MEUR you get x Euros worth of REEF in return.

Users can redeem their MEUR for REEF at any time without limitations. However, a redemption fee might be charged on the redeemed amount.

For example, if the current redemption fee is 1%, the price of REEF is €0.01 and you redeem 100 MEUR, you would get 9,900 REEF (10,000 REEF minus a redemption fee of 100 REEF).

Note that the redeemed amount is taken into account for calculating the base rate and might have an impact on the redemption fee, especially if the amount is large.

### Is a redemption the same as paying back my debt?

No, redemptions are a completely separate mechanism. All one has to do to pay back their debt is adjust their Trove's debt and collateral.

### How is the redemption fee calculated?

Under normal operation, the redemption fee is given by the formula `(baseRate + 0.5%) * REEFdrawn`

### How is the `baseRate` calculated?

Redemption fees are based on the `baseRate` state variable in Mosaic, which is dynamically updated. The `baseRate` increases with each redemption, and decays to 0 over time with a 12 hour half life.

Upon each redemption:

* `baseRate` is decayed based on time passed since the last fee event
* `baseRate` is incremented by an amount proportional to the fraction of the total MEUR supply that was redeemed
* The redemption fee is given by `(baseRate + 0.5%) * REEFdrawn`

`baseRateNew = baseRateOld + redeemedMEUR / (2 * totalMEUR)`

Where `baseRateOld` is the value just prior to this redemption, and `baseRateNew` is the new value (and gets applied to this redemption).

### As a borrower, do I lose money if I'm redeemed against?

If your Trove is redeemed against, you _do not_ incur a net loss. However, you will lose some of your REEF exposure. Your Trove's collateral ratio will also improve after a redemption.

### How can I avoid being redeemed against?

The best way to avoid being redeemed against is by maintaining a high collateral ratio relative to the rest of the Troves in the system. Remember: The riskiest Troves (i.e. lowest collateralized Troves) are first in line when a redemption takes place.
