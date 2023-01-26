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
- https://github.com/fractional-company/modular-fractional/pull/203
- https://github.com/fractional-company/modular-fractional/pull/211
- https://github.com/fractional-company/modular-fractional/pull/201
- https://github.com/fractional-company/modular-fractional/pull/207
- https://github.com/fractional-company/modular-fractional/pull/210
- https://github.com/fractional-company/modular-fractional/pull/206
- https://github.com/fractional-company/modular-fractional/pull/204
- https://github.com/fractional-company/modular-fractional/pull/205
- https://github.com/fractional-company/modular-fractional/pull/200

All wardens participating in this mitigation review have been invited to the [Tessera repo](https://github.com/fractional-company/modular-fractional/); please check your Github notifications to accept the invitation. 
