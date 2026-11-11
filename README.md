# clone-lin-gmx-v2-funding-amount

Experimental LIN clone of GMX V2 `getFundingAmount` (uint64-scale: `mulDiv(size, latest-entry, FLOAT*SQRT, roundUp)` so charge rounds up and claim rounds down).

- **Upstream:** [gmx-io/gmx-synthetics](https://github.com/gmx-io/gmx-synthetics) `contracts/market/MarketUtils.sol` commit `a85ea3491c19c93bb4b5a002d9b358fb769b7849` (GPL-2.0-or-later after BUSL Change Date 2026-08-31).
- **LIN kernel:** [`src/lin_gmx_v2_funding_amount.lin`](src/lin_gmx_v2_funding_amount.lin)
- **C11 oracle copy:** [`test/oracles/gmx_v2_funding_amount_c11.c`](test/oracles/gmx_v2_funding_amount_c11.c)
- **Proofs (lin-open only):** [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) `examples/gmx_v2_funding_amount/` and `python3 test/prove_gmx_v2_funding_amount_external.py`
- **Class:** EXPERIMENTAL. Not Arbitrum GMX V2 uint256. Not FLOAT 1e30. Not a production replacement. Not GMX V1 `getFundingFee` (no SQRT) and not `getFundingAmountPerSizeDelta` (inverse mulDiv).

Named goldens (uint64-scale): size 1e8 latest 5000123 entry 4000000 charges **100013** vs claims **100012** vs V1/applyFactor (no SQRT) **100012300**; dust size 100 charges **1** vs claim **0**; remainder 0 yields **100000** both ways; latest==entry **0**; latest < entry **ok=0** vs signed **-1000000**; 7e9*2e9 **ok=0** vs naive i64 wrap **-4446744073709551616**; inverse 100012*1e9/1e8 **1000120**.
