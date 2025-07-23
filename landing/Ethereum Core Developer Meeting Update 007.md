# Ethereum Core Developer Meeting Update 007

## Arrow Glacier Delay: 90% Merge, 10% Difficulty Bomb 💣

The Ethereum development community has made significant progress toward finalizing the long-anticipated transition to Proof of Stake (PoS). With the **Ethereum Merge** now technically 90% complete, developers have shifted focus to resolving the remaining challenges while managing the Proof of Work (PoW) legacy through the **Arrow Glacier upgrade**. This update dives into the technical architecture of the merged network, the role of key components like the **Engine API**, and the implications for future network stability.

## Arrow Glacier Upgrade 🏹🧊

During the 124th core developer meeting, the community reached consensus on delaying the **difficulty bomb**—a mechanism designed to gradually increase mining difficulty until PoW becomes unviable. The **Arrow Glacier upgrade**, scheduled for activation at block 13,773,000 (approximately December 8, 2021), implements **EIP-4345** to postpone the bomb until mid-2022. This delay provides developers with critical time to finalize the Merge while minimizing disruptions to existing PoW operations.

> **Key Insight**: The difficulty bomb and the Merge are independent processes. While the bomb's activation would eventually force a transition to PoS, the Merge itself requires a separate network upgrade based on the **Terminal Total Difficulty (TTD)** threshold. This separation allows developers to prioritize stability without relying on the bomb as a deadline.

## Post-Merge Architecture Overview 🏗

The Ethereum Merge leverages two existing client layers:  
1. **Execution Layer (formerly Eth1)**: Handles transaction execution, smart contract operations, and state management.  
2. **Consensus Layer (formerly Eth2)**: Manages PoS validation, block finality, and network security.  

By integrating these layers, the merged network maintains backward compatibility with existing Ethereum applications while introducing PoS efficiency. Node operators must run both clients to maintain a fully validating node.

👉 [Explore Ethereum's future with OKX](https://bit.ly/okx-bonus)

### Beacon Node: The Consensus Engine 🚨

The Beacon Node, responsible for PoS consensus, now monitors the PoW chain for the **TTD threshold**. Once a block exceeds this difficulty, it becomes the final PoW block. Subsequent blocks are validated by PoS validators. This transition requires the Beacon Node to interact with the Execution Layer via the **Engine API** to generate and verify **Execution Payloads**—the PoS-era equivalent of PoW blocks.

### Engine API: Bridging Consensus and Execution ⚙️

The **Engine API** (defined in [execution-apis](https://github.com/ethereum/execution-apis)) introduces three critical methods for inter-client communication:  

| Method                  | Function |
|------------------------|----------|
| `engine_executePayload` | Validates Execution Payloads against protocol rules. |
| `engine_forkchoiceUpdated` | Communicates chain head updates and finality. |
| `engine_getPayload`       | Retrieves constructed Execution Payloads for block proposals. |

This API ensures seamless coordination between layers, enabling validators to propose and verify blocks while maintaining state consistency.

## Execution Layer: State Management and Transaction Processing 🛠

The Execution Layer retains core Ethereum functionalities but adapts to PoS requirements:  
- **Block Format Changes**: PoW-specific fields (e.g., `difficulty`, `nonce`) are deprecated.  
- **Fee Distribution**: Transaction fees now go to a `feeRecipient` address instead of block rewards.  
- **Network Protocol Updates**: PoW block broadcasting (via `NewBlockHashes` and `NewBlock` messages) is removed.  

Validators now rely on the Consensus Layer for block proposal rights, while the Execution Layer focuses on state transitions and transaction execution.

## P2P Network and Synchronization 📡

Post-Merge, both layers operate on separate P2P networks:  
- **Consensus Layer**: Broadcasts attestations, slashings, and Beacon Blocks.  
- **Execution Layer**: Propagates transactions and state updates.  

Synchronization strategies are evolving to handle edge cases during the transition. Developers continue testing these mechanisms on the **Pithos testnet**, with plans for a community update in the coming weeks.

## Frequently Asked Questions ❓

### 1. What Happens to Ethereum Miners After the Merge?
Miners will no longer validate blocks once the TTD threshold is reached. However, Ethereum's supply issuance will shift from mining rewards to staking rewards for validators.

### 2. How Do Users Experience the Merge?
End-users will notice no immediate changes in dApp functionality. Gas fees and transaction speeds depend on Layer 2 scaling solutions rather than the consensus transition.

### 3. What Are Execution Payloads?
Execution Payloads encapsulate transaction data and state changes in the PoS network, replacing PoW blocks. They include fields like `timestamp`, `baseFeePerGas`, and `feeRecipient`.

### 4. Can the Difficulty Bomb Still Affect the Merge Timeline?
While the Arrow Glacier delay postpones the bomb until 2022, developers retain the option to adjust TTD if further delays occur. The Merge and bomb remain technically decoupled.

### 5. What Role Does the Beacon Chain Play?
The Beacon Chain coordinates PoS validators, manages slashing penalties, and finalizes blocks. It becomes the network's primary consensus engine post-Merge.

👉 [Stay updated on blockchain innovations with OKX](https://bit.ly/okx-bonus)

## Roadmap and Testing 🔧

With the **Amphora milestone** completed, developers are finalizing specifications for the Execution Layer and Engine API. The **Pithos testnet** serves as a critical testing ground, simulating multi-client compatibility across real-world conditions. A community coordination meeting is planned to align infrastructure providers ahead of the Mainnet launch.

The Merge represents a pivotal step toward Ethereum's vision of scalability and sustainability. By decoupling consensus from execution, the network lays the groundwork for future upgrades like sharding and EIP-4444. As the TTD threshold approaches, the community remains vigilant in ensuring a seamless transition for all stakeholders.