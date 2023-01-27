# Tessera - Versus Mitigation Review
- Total Prize Pool: $8,700 USDC
- [Warden guidelines for C4 mitigation reviews](https://code4rena.notion.site/Guidelines-for-Versus-mitigation-reviews-ed10fc5cfbf640bd8dcec66f38b343c4)
- Submit findings [using the C4 form](https://code4rena.com/contests/2023-01-tessera-versus-mitigation-contest/submit)
- Starts January 27, 2023 20:00 UTC
- Ends February 1, 2023 20:00 UTC

## Important note 

Each warden must submit a mitigation review for *every High and Medium finding* from the parent contest. **Incomplete mitigation reviews will not be eligible for awards.**

# Findings being mitigated

- [H-01: GroupBuy does not check return value of call](https://github.com/code-423n4/2022-12-tessera-findings/issues/6)
- [H-02: GroupBuy: Lost ETH when the NFT is bought for less than the minimum reserve price](https://github.com/code-423n4/2022-12-tessera-findings/issues/7)
- [H-03: Groupbuy: _verifyUnsuccessfulState and _verifySuccessfulState both can return true when block.timestamp == pool.terminationPeriod](https://github.com/code-423n4/2022-12-tessera-findings/issues/10)
- [H-04: OptimisticListingSeaport.propose sets pendingBalances of newly added proposer instead of previous one](https://github.com/code-423n4/2022-12-tessera-findings/issues/12)
- [H-05: Attacker can DOS OptimisticListing with very low cost](https://github.com/code-423n4/2022-12-tessera-findings/issues/25)
- [H-06: Funds are permanently stuck in OptimisticListingSeaport.sol contract if active proposal is executed after new proposal is pending.](https://github.com/code-423n4/2022-12-tessera-findings/issues/43)
- [H-07: User loses collateral converted to pendingBalance when cash() or list() is called](https://github.com/code-423n4/2022-12-tessera-findings/issues/44)
- [H-08: Attacker can steal the amount collected so far in the GroupBuy for NFT purchase.](https://github.com/code-423n4/2022-12-tessera-findings/issues/47)
= [H-09: GroupBuy can be drained of all ETH.](https://github.com/code-423n4/2022-12-tessera-findings/issues/52)
- [M-01: GroupBuy may purchase NFT not in the allowed list](https://github.com/code-423n4/2022-12-tessera-findings/issues/14)
- [M-02: Attacker can delay proposal rejection](https://github.com/code-423n4/2022-12-tessera-findings/issues/24)
- [M-03: Users that send funds at a price lower than the current low bid have the funds locked](https://github.com/code-423n4/2022-12-tessera-findings/issues/31)
- [M-04: Priority queue min accounting breaks when nodes are split in two](https://github.com/code-423n4/2022-12-tessera-findings/issues/32)
- [M-05: Orders may not be fillable due to missing approvals](https://github.com/code-423n4/2022-12-tessera-findings/issues/36)
- [M-06: Only one GroupBuy can ever use USDT or similar tokens with front-running approval protections](https://github.com/code-423n4/2022-12-tessera-findings/issues/37)
- [M-07: Loss of ETH for proposer when it is a contract that doesn't have fallback function.](https://github.com/code-423n4/2022-12-tessera-findings/issues/40)
- [M-08: Earlier bidders get cut out of future NFT holdings by bidders specifying the same price.](https://github.com/code-423n4/2022-12-tessera-findings/issues/45)
- [M-09: GroupBuys that are completely filled still don't raise stated target amount](https://github.com/code-423n4/2022-12-tessera-findings/issues/49)

# Mitigations to be reviewed

All PRs are linked in the comments of the above-listed findings, but here is the full list of PRs for ease of reference:

- https://github.com/fractional-company/modular-fractional/pull/202
    - Addresses [12](https://github.com/code-423n4/2022-12-tessera-findings/issues/12) Updated pendingBalances mapping before setting the newly proposed listing. This way, the balance is updated for the previous proposer and the currently proposed listing can be overridden with the new one.
- https://github.com/fractional-company/modular-fractional/pull/203
    - Addresses [10](https://github.com/code-423n4/2022-12-tessera-findings/issues/10) Updated comparison to use <= to avoid edge case for an invalid state. 
- https://github.com/fractional-company/modular-fractional/pull/211
    - Addresses [43](https://github.com/code-423n4/2022-12-tessera-findings/issues/43) Solution is to move orderHash to Listing struct so that active and proposed listings can have separate order hashes.
- https://github.com/fractional-company/modular-fractional/pull/201
    - Addresses [47](https://github.com/code-423n4/2022-12-tessera-findings/issues/47) Fixed by moving success state update before call to market buyer
- https://github.com/fractional-company/modular-fractional/pull/207
    - Addresses [7](https://github.com/code-423n4/2022-12-tessera-findings/issues/7) Calculate actual minReservePrice after purchase has been made. This is done by simply dividing total filled quantity by the purchase price. This fixes the ETH accounting when the NFT is purchased for less than the minimum reserve price. 
- https://github.com/fractional-company/modular-fractional/pull/212
    - Addresses [32](https://github.com/code-423n4/2022-12-tessera-findings/issues/32) Used <= when comparing the new price to the lowest bid price. That way, it can only override the lower bid if price is higher. 
- https://github.com/fractional-company/modular-fractional/pull/213
    - Addresses [49](https://github.com/code-423n4/2022-12-tessera-findings/issues/49) where due to truncation, the stated minimum raised wouldn't result in actually being able to purchase with the full amount raised. Instead of doing that math we’re going to have the initial purchase by the deployer set the initial target. 
- https://github.com/fractional-company/modular-fractional/pull/206
    - Addresses [31](https://github.com/code-423n4/2022-12-tessera-findings/issues/31) If total supply is equal to filled quantities, use min reserved price instead of min price when validating the user contribution. this way, funds will not be stuck until a purchase is made and the user will be able to withdraw their funds right away.
- https://github.com/fractional-company/modular-fractional/pull/204
    - Addresss [6](https://github.com/code-423n4/2022-12-tessera-findings/issues/6) Fixed by checking success value of call
- https://github.com/fractional-company/modular-fractional/pull/205
    - Addresses [33](https://github.com/code-423n4/2022-12-tessera-findings/issues/33) Validated the NFT on pool creation to prevent funds from being locked until the termination period has passed.

All wardens participating in this mitigation review have been invited to the [Tessera repo](https://github.com/fractional-company/modular-fractional/); please check your Github notifications to accept the invitation. 
