# FreeStable: Stablecoin & Lending Design

FreeStable is a protocol for decentralised and collateralized stablecoins.

The design can be used for a stablecoin for any fiat currency.

**Brief functionality overview:**

- Collateralized with ETH
- A single Vault for an address
- Regular debt repayments ([instalment debt](https://www.investopedia.com/terms/i/installmentdebt.asp))
- Liquidation only if a minter skips their debt repayment AND the collateralization ratio is below a threshold
- Burning fee instead of an interest rate

The variables that the governance (DAO) can change:

- minting ratio
- collateralization ratio
- burning fee
- instalment frequency (how often do debt instalments need to be paid, for example once per month, once per week etc.)
- the minimum instalment amount
- total stablecoin supply cap (could also be *total collateral cap*)
- DAO token rewards for minters

The system bears some similarities with MakerDAO and Synthetix, but also has important differences (regular debt repayments, additional liquidation protection, burning fee etc.)

## Minting

A user (minter) mints a new stablecoin by locking up a certain amount of ETH (collateral). The minting ratio is not necessarily 1:1 (100%), but likely higher - depending on what the DAO decides (a 120% ratio seems reasonable).

Note that the amount of locked collateral does not change with the collateral price swings (as it is the case with Synthetix). If the collateral price would rise by 100%, the minter wouldn't be able to just unlock half of the collateral without any debt repayment. Synthetix, on the other hand, allows this.

## Burning

Burning means sending stablecoin tokens back to the stablecoin contract (using the burn function) and receiving (some of) the collateral back. Example: If minter repays back 30% of their stablecoin debt, they get back 30% of their ETH collateral.

A minter needs to regularly burn stablecoins, otherwise they might risk having their position liquidated. 

## Liquidations

A liquidation can occur when a minter hasn't made a debt repayment instalment in the required time, AND their collateralization ratio is below threshold.

These requirements protect minters from accidental/black swan liquidations such as the one with MakerDAO in March 2020.

> Potential feature: If the collateralization ratio (of some collateral eligible to be liquidated) is below 100%, the liquidator could be rewarded with governance tokens whose value bridges the missing collateralization ratio gap. Maker has a similar feature.

## Mechanisms to keep the peg

### Stablecoin price

A low stablecoin price (below the peg) incentivized minters to buy stablecoin in order to repay the debt cheaply. On the other hand, a high stablecoin price incentivizes minters to mint more stablecoins and sell them.

### Regular debt repayments

(New) stablecoins usually suffer from their price being below the peg, due to low demand. That's where the mechanism for regular debt repayments comes useful. It incentivizes minters to regularly buy (back) stablecoins in order to pay debt instalments and avoid being liquidated.

### Burn fee

If the burn fee is low, minters are incentivized to repay their debt more often and in bigger quantities. The higher burn fee would incentivize minters to make smaller debt repayments (closer to the required minimum and time frequency).

### DAO token rewards

Another issue that new stablecoins face is incentivizing people to become minters. A common approach currently is to incentivize them with rewards in the governance tokens. This also helps distributing tokens to actual users of the protocol.

## Redeemability

Redeeming is the ability to swap a stablecoin for its underlying collateral.

It's worth knowing that no stablecoin has complete/unconditional redeemability. 

Centralized stablecoins like USDC and TUSD have minimum amounts set up (TUSD - $1000, USD - $100) in order to redeem fiat currency for the stablecoin. And they also do KYC.

USDT says it is redeemable and it kind of allows it, but it's not 100% collateralized (only 74%). It also has hefty fees for redeeming USDT, though.

Decentralised collateralised stablecoins (like DAI, sUSD, and also FreeStable) allow redeeming in two different ways:

- Burning: a minter burns stablecoin (repays debt) to get back the collateral.
- Liquidation: anyone can burn stablecoin in order to get a certain minter's collateral (under certain conditions).

Algorithmic stablecoins (a new kind of decentralised stablecoins) don't have any redeemability at all, because there's no collateral involved.
