# Borrowing

### **Why would I use Mosaic for borrowing?**

Mosaic protocol offers interest-free loans and is more capital efficient than other borrowing systems (i.e. less collateral is needed for the same loan). Instead of selling REEF to have liquid funds, you can use the protocol to lock up your REEF, borrow against the collateral to withdraw MEUR, and then repay your loan at a future date.

For example: Borrowers speculating on future REEF price increases can use the protocol to leverage their REEF positions up to `11 times`, increasing their exposure to price changes. This is possible because MEUR can be borrowed against REEF, sold on the open market to purchase more REEF — rinse and repeat.\*

\*_Note: This is not a recommendation for how to use Mosaic. Leverage can be risky and should be used only by those with experience._

### **What do you mean by collateral?**

Collateral is any asset which a borrower must provide to take out a loan, acting as a security for the debt. Currently, Mosaic only supports REEF as collateral.

### Is REEF the only collateral accepted by Mosaic?

Yes, REEF is the _only_ collateral type accepted by Mosaic.

### **How can the protocol offer interest-free borrowing?**

The protocol charges one-time borrowing and redemption fees that algorithmically adjust based on the last redemption time. For example: If more redemptions are happening (which means MEUR is likely trading at less than €1), the borrowing fee would continue to increase, discouraging borrowing.

Other systems require variable interest rates to make borrowing more or less favorable, but do so implicitly since borrowers would not feel the impact upfront. Given that this also needs to be managed via governance, Mosaic instead opts for a fully decentralized and direct feedback mechanism via one-off fees.

### **How can I borrow with Mosaic?**

To borrow you must open a Trove and deposit a certain amount of collateral (REEF) to it. Then you can draw MEUR up to a collateral ratio of `110%`. A **minimum debt** of `200 MEUR` is required.

### **What is a Trove?**

A Trove is where you take out and maintain your loan. Each Trove is linked to a Reef Chain address and each address can have just one Trove. If you are familiar with Vaults or CDPs from other platforms, Troves are similar in concept.

Troves maintain two balances: one is an asset (REEF) acting as collateral and the other is a debt denominated in MEUR. You can change the amount of each by adding collateral or repaying debt. As you make these balance changes, your Trove's collateral ratio changes accordingly.

You can close your Trove at any time by fully paying off your debt.

### **Do I have to pay fees as a borrower?**

Every time you draw MEUR from your Trove, a one-off borrowing fee is charged on the drawn amount and added to your debt. Please note that the borrowing fee is variable (and determined algorithmically) and has a minimum value of `0.5%` under normal operation. The fee is `0%` during [Recovery Mode](recovery-mode.md).

A `2 MEUR` [Liquidation Reserve](borrowing.md#what-is-the-liquidation-reserve) charge will be applied as well, but returned to you upon repayment of debt.

Another consideration is the price of MEUR at the time of repayment. If at the time you want to repay your loan MEUR is trading at €1.02 on the market and you need to buy it, you are incurring a 2% 'fee'. You can avoid this by having your borrowed funds readily available or by being able to wait for MEUR to return to peg.

### **How is the borrowing fee calculated?**

The borrowing fee is added to the debt of the Trove and is given by a `baseRate`. The fee rate is confined to a range between `0.5%` and `5%` and is multiplied by the amount of liquidity drawn by the borrower.

For example: The borrowing fee stands at `0.5%` and the borrower wants to receive `400 MEUR` to their wallet. Being charged a borrowing fee of `2.00 MEUR`, the borrower will incur a debt of `404 MEUR` after the Liquidation Reserve and issuance fee are added.

### **When do I need to pay my loan back?**

Loans issued by the protocol do not have a repayment schedule. You can leave your Trove open and repay your debt any time, as long as you maintain a collateral ratio of at least `110%`.

### What is the collateral ratio?

This is the ratio between the Euro value of the collateral in your Trove and its debt in MEUR. The collateral ratio of your Trove will fluctuate over time as the price of REEF changes. You can influence the ratio by adjusting your Trove's collateral and/or debt — i.e. adding more REEF collateral or paying off some of your debt.

For example: Let's say the current price of REEF is `€0.01` and you decide to deposit `100,000 REEF`. If you borrow `500 MEUR`, then the collateral ratio for your Trove would be `200%`.

$$\frac{100,000 \ REEF \ * \ €0.01}{500 \ MEUR} * 100\% = 200\%$$

If you instead took out `833 MEUR` that would put your ratio at `120%`.

### **What is the minimum collateral ratio (MCR) and the "recommended" collateral ratio?**

The minimum collateral ratio (or MCR for short) is the lowest ratio of debt to collateral that will not trigger a liquidation under normal operations (aka Normal Mode). This is a protocol parameter that is set to `110%`. So if your Trove has a debt of `1,000 MEUR`, you would need at least `€1,100` worth of REEF posted as collateral to avoid being liquidated.

To avoid liquidation during [Recovery Mode](recovery-mode.md), it is recommended to keep ratio comfortably above `150%` (e.g. `200%` or better `250%`).

### **What happens if my Trove is liquidated?**

You lose your collateral as your debt is paid off through [liquidation](stability-pool-and-liquidations.md#what-are-liquidations), i.e. you will no longer be able to retrieve your collateral by repaying your debt. A liquidation thus results in a net loss of `9.09% (= 100% * 10 / 110)` of your collateral's Euro value.

### **What is the Liquidation Reserve?**

When you open a Trove and draw a loan, `2 MEUR` is set aside as a way to compensate gas costs for the transaction sender in the event your Trove being liquidated. The Liquidation Reserve is fully refundable if your Trove is not liquidated, and is given back to you when you close your Trove by repaying your debt. The Liquidation Reserve counts as debt and is taken into account for the calculation of a Trove's collateral ratio, slightly increasing the actual collateral requirements.

### **What happens if my Trove is redeemed against?**

When MEUR is redeemed, the REEF provided to the redeemer is allocated from the Trove(s) with the lowest collateral ratio (even if it is above `110%`). If at the time of redemption you have the Trove with the lowest ratio, you will give up some of your collateral, but your debt will be reduced accordingly.

The Euro value by which your REEF collateral is reduced corresponds to the nominal MEUR amount by which your Trove's debt is decreased. You can think of redemptions as if somebody else is repaying your debt and retrieving an equivalent amount of your collateral. As a positive side effect, redemptions improve the collateral ratio of the affected Troves, making them less risky.

Redemptions that do not reduce your debt to 0 are called partial redemptions, while redemptions that fully pay off a Trove's debt are called full redemptions. In such a case, your Trove is closed, and you can claim your collateral surplus and the Liquidation Reserve at any time.

Let's say you own a Trove with `200,000 REEF` collateralized and a debt of `1,600 MEUR`. The current price of REEF is `€0.01`. This puts your collateral ratio (CR) at `125% (= 100% * (200,000 * 0.01) / 1,600)`. Let's imagine this is the lowest CR in the Mosaic system and look at two examples of a partial redemption and a full redemption:

**Example of a partial redemption**

Somebody redeems `600 MEUR` for `60,000 REEF` and thus repays `600 MEUR` of your debt, reducing it from `1,600 MEUR` to `1,000 MEUR`. In return, `60,000 REEF,` worth `€600`, is transferred from your Trove to the redeemer. Your collateral goes down from `200,000 to 140,000 REEF`, while your collateral ratio goes up from `125%` to `140% (= 100% * (140,000 * 0.01) / 1,000)`.

**Example of a full redemption**

Somebody redeems `3,000 MEUR` for `300,000 REEF`. Given that the redeemed amount is larger than your debt minus `2 MEUR` (set aside as a Liquidation Reserve), your debt of `1,600 MEUR` is entirely cleared and your collateral gets reduced by `€1,598` of REEF, leaving you with a collateral of `40,200 REEF (= 200,000 - 159,800)`.

### How can you offer a collateral ratio as low as 110%?

By making liquidation instantaneous and more efficient, Mosaic needs less collateral to provide the same security level as similar protocols that rely on lengthy auction mechanisms to sell off collateral in liquidations.

### **How can I take advantage of leverage?**

You can sell the borrowed MEUR on the market for REEF and use the latter to top up the collateral of your Trove. That allows you to draw and sell more MEUR, and by repeating the process you can reach the desired leverage ratio.

Assuming perfect price stability (`1 MEUR = €1`), the maximum achievable leverage ratio is `11x`. It is given by the formula:

maximum leverage ratio = $$\frac{MCR}{(MCR - 100\%)}$$ where MCR is the Minimum Collateral Ratio.

### **Why did the collateral and debt of my Trove increase without my intervention?**

If Troves are liquidated and the Stability Pool is empty (or gets emptied due to the liquidation), every borrower will receive a portion of the liquidated collateral and debt as part of a redistribution process.
