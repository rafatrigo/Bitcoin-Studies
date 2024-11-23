#bitcoin #mastering-bitcoin-seminar-21 

Chapter 6, 7

# Questions

## What are the different components of a Bitcoin transaction?

- Version
	The transaction must follows the rules of the version
- Marker
- Flag
- Inputs
	The input field has others fields.
	- Count
		Number of inputs in the transaction >= 1
	- Previous output txid
	- Previous output index
	- Length
	- Sequence
- Outputs
	The output field has others fields.
	- Count
	- Amount
	- Length
	- Output script
		The conditions that need to be fulfilled in order to spend the bitcoins
- Witness structure
- Lock time

## What are transaction inputs, and how are they constructed? What are unlocking scripts?

- Reference to a previous transaction (txid)
- The output of the previous transaction that is being used as an input.
- ScriptSig (unloking script)
	This is the script used to unlock the Bitcoins being spent. It proves that the sender has the right to spend the Bitcoin referenced by the input.
	- Digital signature create by the sender
	- The public key of the sender
- Sequence number

## What parts of the transaction structure got affected with the segwit upgrade? Were there any new fields added to the transaction structure?

The key goals of SegWit were to fix transaction malleability, increase the block size limit, and improve scalability.

- Separation of Witness Data (Segregation of Signature Data)
- Marker and Flag
- Witness data

## Compare a coinbase transaction to a normal bitcoin transaction and highlight the differences between the two.

## What are UTXOs (Unspent Transaction Outputs), and how is the balance of a wallet calculated?

## What is the difference between a locking script (scriptPubKey) and an unlocking script (scriptSig)? What is the difference between a redeem script and a witness script?

**Locking script**
The locking script (also known as **scriptPubKey**) is the script included in the **output** of a Bitcoin transaction. It specifies the conditions that must be met to spend the Bitcoin in a future transaction. Defining who is eligible to spend it.

**Unlock script**
The unlocking script (also known as **scriptSig**) is included in the **input** of a Bitcoin transaction and is used to satisfy the conditions set by the corresponding locking script (scriptPubKey) in a previous transaction output.

## What's P2PKH? How is it built?

## What's P2SH? How is it built? What are the benefits of using P2SH over P2PKH? What are the drawbacks?

## What's a scripted multisignature script? How is it built?
