#bitcoin #bitcoin-book 

### Transaction
Tells the network that the owner of certain bitcoins has authorized the transfer of that value to another owner.

#### Inputs
- Each transaction contains one or more **inputs**, which spend funds.
- Each transaction also contains one or more **outputs**, which receive funds.
- Output is slightly less than inputs and the diference is the transaction fee.
- The **fee** is a small payment collected by the miner.
- The transaction also contains **proof of ownership** for each amount of bitcoin being spend.
- The proof of ownership is a key from the owner, which can be validated by anyone.

#### Transaction chains
When the **output** of a transaction is the **input** of another transaction.

Imagine you received 1BTC, that's an output transaction with your address. Now if you want to send 0,5BTC to someone you references the output as the input of the new transaction (this reference is a 32-bytes transaction identifier (txid)). Now you have the transaction input, and the output will be the 0,5BTC with the address of the wallet you send it to and something less than 0,5BTC which is the change minus the fee.

#### Change
- In addition of one or more outputs that pay the receiver of bitcoins, some transactions also have a output that pays the spender of bitcoins, called a **change output**.
- In the Bitcoin Protocol there is no difference between a change output and a payment output.
- The change address doesn't have to be the same address as the input, for privacy reasons, is often a new address for the owner's wallet.

#### Coin Selection
- Different wallets handle which input to use in a payment using different strategies.
- They might aggregate many small inputs, or use one that is equal to or larger than the desired payment.

#### Common Transaction Forms

##### Simple Payment
One input and two outputs.

Input: Value possessed.
Output 1: Value send.
Output 2: Change.

##### Aggregating Transaction
Various inputs and one output.

##### Distributing Transaction
One input and various outputs.

### Construction a Transaction

- The wallet application already contains the the logic for selecting inputs and generating outputs.
- The user only needs to select an amount, destination and fee.
- If a wallet knows all the inputs it controls, it can create a transaction even if it is offline.
- Transactions doesn't need to be constructed and signed while connected to the Bitcoin Network.

#### Getting  the Right Inputs

- First the wallet will have to find inputs that have the amount of bitcoin you want to pay.
- Most of the wallets keep track of all the available outputs belonging to the address in the wallet.
- A bitcoin wallet that runs on a **full node** contais all the confirmed transactions.
- Full nodes needs a lot of resources, so many wallets run **lightweight clients** that tracks only the user's own transactions.
- UTXO: unspent transaction output (a receiving transaction).

#### Creating the Outputs

- A transaction output is created with a script that says something like, "This output is paid to whoever can present a signature from the key corresponding to receiver public address."

#### Adding the Transaction to the Blockchain

The transaction created by Alice’s wallet application contains everything necessary to confirm ownership of the funds and assign new owners.

##### How It Propagates

- The wallet send the transaction to a **bitcoin node**.
- The sender wallet doesn't need to be connected to the receiver's wallet.
- Any Bitcoin node that receives a valid transaction it has not seen before will forward it to all other nodes to which it is connected, a propagation technique known as **_gossiping_**.
- The transaction propagate across the peer-to-peer network, reaching a large percentage of the nodes within few seconds.

### Bitcoin Mining

After a transaction is propagated on the Bitcoin network it doesn't become part of the **blockchain** until it is included in a block through mining and the block has been **validated** by a full node.

- Transactions are bundled into blocks.
- Blocks have a very small header that must be formed in a very specific way.
- Headers require a **enormous** amount of computation to be created.
- Headers require a **small** amount of computation to be verified.

#### Purpose

- Secure the blockchain validating blocks of transactions.
- Mining currently creates new bitcoins in each block.

Mining is designed to be a **decentralized lottery**. Each miner can create their own lottery ticket by create a candidate block. The miner **hashes** the candidate block data, if the output of the hash function matches a template determined by the Bitcoin protocol, the miner wins the lottery and Bitcoin users will accept the block with its transactions as a valid block. If the output doesn't match the template, the miner makes a small change to their candidate block and tries again.
The number of candidate blocks that can be created is about 168 billion trillion.
However, after a correct block is created anyone can verify if the block is valid by running the hash function only once.

- Each miner includes a special transaction in their candidate blocks, one that pays their own Bitcoin address the block reward plus the sum of transaction fees from all the transactions included in the candidate block.
- Miners that participate in a **mining pool** have set up their software to assign the reward to a **pool address**, after that a share of the reward is distributed to members of the poll, in proportion to their work.

#### Block Depth
The amount of blocks **above** a certain block.

#### Block Height
The amount of blocks **bellow** a certain block.

If there are multiple alternative blocks to chose from the full node will chose the block that has more prove of work (PoW). In other words the block with more **depth**. Because more blocks already have validated this block, increasing the security of the blockchain.
