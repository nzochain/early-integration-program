# Supported networks

NZOChain scan and related EVM risk flows currently cover **four** networks.

| Network | API `network` value |
|---|---|
| Ethereum | `ethereum` |
| BNB Chain | `bnb` |
| Polygon | `polygon` |
| Arbitrum | `arbitrum` |

For transaction analyze, `chainId` is used (example from docs: `1` for Ethereum). Map chain IDs carefully in your integration; do not invent unsupported chains.

---

## Not supported (identified scan engine)

- **Solana** — not supported
- **Base** — not currently supported by the identified scan engine

Do not document Solana or Base as live scan networks in this release.

---

## Related

- [PRODUCT-STATUS.md](../PRODUCT-STATUS.md)
- https://docs.nzochain.com/networks/overview
