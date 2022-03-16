## Cosmos
Most blockchains have:
1. Shared execution layer
2. Smart contracts

Ethereum developers just play around in smart contracts, don't need to worry about consensus, etc.
"The big brain giga-chads nerdsniped me into Cosmos"
- Scott Sunarto

## What do I mean when I saw Cosmos?
- Not Cosmos Hub
- Not $ATOM (No money for you)
- Cosmos SDK: Tendermint Consensus + IBC Modules + other stuff

### Philosophy
- Instead of shared execution layer, you want application specific chains.
- Benefit 1: You have control. :vader. 
    - Precompiles - code that denotes complicated computations cheaper on chain. If you don't have a precompile, you need to use the evm. E.g. cryptography. Defined in clients Cacn technically use .com domain as ENS, but this is extremely expensive to do DNSSEC onchain since cryptography isn't on chain. Might cost $1000 some money to verify
    - Novel consensus/Protocol Design. Osmosis wants to prevent MEV from happening; they want to use threshold encryption to do so. Thus, Osmosis can embed this in their chain
- Benefit 2: Blockspace Monopoly
    - Vertical Scaling brings problems like state bloat, computation power. Solana drops Merkle trees from client design to improve L1 scaling.
    - Cosmos Approach: Instead of scaling vertically, you can create your own blockchain and scale horizontally. If each application has their own separate throughput, Polygon doesn't get rekt bc people are playing sunflower games.

## IBC
- relies on instant finality
- TCP/IP - not a bridge
- easy to add Cosmos based blockchains and other blockchains with {easy way to create light client proofs, Relayer}
- peg zone
- **Relayer**: trustless way to send data from one blockchain to another. Think of it as a cable that can transmit data from one chain to another. Security comes from the light client proof, relayers have no verification.
End Goal: Each wallet is its own relayer. Relayers also get transaction fees in the future. Currently, relayers are subsidized via the Interchain foundation(Ethereum foundation equivalent)
- No flash loans, flash mints, flash anything via IBC bc that requires atomicity.
- Can do token transfers, cross chain swaps

![](/media/Research/IBCpic.png)

Wat is IBC

# Questions

## Subnets vs Cosmos
- There is an expectation that you share security with Avalanche. Problem is that shared security isn't free, you need to pay avalanche validators for this. 
- Tendermint is novel: instant finality + 2/3 network validators needs to be aligned. Instant finality is huge because it simplifies multichain consensus. In a proof of work blockchain, by the virtue of a 51% attack, blocks are not final since you can end up with uncle blocks[reorgs](https://medium.com/dragonfly-research/dr-reorg-or-how-i-learned-to-stop-worrying-and-love-mev-2ee72b428d1d)
    - This is bad for bridges because a transaction where you burn a token to mint it via a bridge to a different chain can be reverted due to a reorg.
        - bridge UX gets killed
    - Multihop dexes can take a very long time because you need to wait for probabilistic finality.
- Are there Oracles natively in Cosmos?
    - No current oracles, but can built oracle chain <-- big brain project right here