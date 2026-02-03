# Community Resources

## Official Channels

- [Website](https://mosaic.markets)
- [Discord](https://discord.gg/KJ89PuzvkJ)
- [Telegram](https://t.me/mosaicnews)
- [X (Twitter)](https://x.com/mosaicprotocol)

## Reef Chain Ecosystem

Mosaic is built on Reef Chain and integrates with the broader Reef ecosystem:

- [ReefSwap](https://reefswap.com/) - Decentralized exchange on Reef Chain
- [Sqwid](https://sqwid.app/) - NFT marketplace on Reef Chain
- [Klever](https://klever.io/) - Wallet supporting Reef Chain

## Diagrams

**Overview of Mosaic Protocol (Normal Mode)**

The system operates in Normal Mode when the Total Collateral Ratio (TCR) is above 150%. In this state:
- Troves can be liquidated when their collateral ratio falls below 110%
- Standard borrowing and redemption fees apply
- Users can open new Troves with a minimum collateral ratio of 110%

**Overview of Mosaic Protocol (Recovery Mode)**

Recovery Mode activates when the TCR falls below 150%. During Recovery Mode:
- Troves with collateral ratio below 150% can be liquidated
- Borrowing fees are set to 0% to encourage collateral top-ups
- The system incentivizes users to restore the TCR above 150%

**How Funds Flow in Mosaic**

1. **Borrowers** deposit REEF collateral and borrow MEUR
2. **Stability Providers** deposit MEUR to the Stability Pool, earning REEF from liquidations and MSIC rewards
3. **MSIC Stakers** stake MSIC to earn protocol fees in MEUR and REEF
