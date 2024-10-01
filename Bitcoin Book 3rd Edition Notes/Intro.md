#bitcoin #bitcoin-book

##### Bitcoin Control Keys
- Allow to prove bitcoin ownership on the network.
- These keys can sign transactions.
- Keys are often stored in a digital wallet on each user's computer or smartphone.
- Possession of a key that can sign transactions is the only prerequisite to spending bitcoin.
- "Your keys, your coins. Not your keys, not your coins."

##### Bitcoin
- A distributed peer-to-peer system (Bitcoin protocol).
- NO central server or point of control.
- Units of bitcoin are created through "mining".
- A public transaction journal (blockchain).
-  A set of rules for independent transaction validation and currency issuance (consensus rules).
- A mechanism for reaching global decentralized consensus on the valid blockchain (proof-of-work algorithm).

##### Mining
- Performing a computational task that references a list of recent bitcoin transactions
- Any participant in the bitcoin network may operate as a miner.
- Mining is use your computing devices to help **secure** transactions.
- Miners are rewarded with both bitcoin and the fees paid by recent transactions.

##### Wallet
- Most common way to access the Bitcoin protocol.

##### Wallet types

Bitcoin wallets can be categorized as follows, according to the platform:

###### Desktop wallet

A desktop wallet was the first type of Bitcoin wallet created as a reference implementation. Many users run desktop wallets for the features, autonomy, and control they offer. Running on general-use operating systems such as Windows and macOS has certain security disadvantages, however, as these platforms are often insecure and poorly configured.

###### Mobile wallet

A mobile wallet is the most common type of Bitcoin wallet. Running on smart-phone operating systems such as Apple iOS and Android, these wallets are often a great choice for new users. Many are designed for simplicity and ease-of-use, but there are also fully featured mobile wallets for power users. To avoid downloading and storing large amounts of data, most mobile wallets retrieve information from remote servers, reducing your privacy by disclosing to third parties information about your Bitcoin addresses and balances.

###### Web wallet

Web wallets are accessed through a web browser and store the user’s wallet on a server owned by a third party. This is similar to webmail in that it relies entirely on a third-party server. Some of these services operate using client-side code running in the user’s browser, which keeps control of the Bitcoin keys in the hands of the user, although the user’s dependence on the server still compromises their privacy. Most, however, take control of the Bitcoin keys from users in exchange for ease-of-use. It is inadvisable to store large amounts of bitcoin on third-party systems.

###### Hardware signing devices

Hardware signing devices are devices that can store keys and sign transactions using special-purpose hardware and firmware. They usually connect to a desktop, mobile, or web wallet via USB cable, near-field-communication (NFC), or a camera with QR codes. By handling all Bitcoin-related operations on the specialized hardware, these wallets are less vulnerable to many types of attacks. Hardware signing devices are sometimes called "hardware wallets", but they need to be paired with a full-featured wallet to send and receive transactions, and the security and privacy offered by that paired wallet plays a critical role in how much security and privacy the user obtains when using the hardware signing device.

##### Full Node vs Lightweight

Another way to categorize Bitcoin wallets is by their degree of autonomy and how they interact with the Bitcoin network:

###### Full node

A full node is a program that validates the entire history of Bitcoin transactions (every transaction by every user, ever). Optionally, full nodes can also store previously validated transactions and serve data to other Bitcoin programs, either on the same computer or over the internet. A full node uses substantial computer resources—​about the same as watching an hour-long streaming video for each day of Bitcoin transactions—​but the full node offers complete autonomy to its users.

###### Lightweight client

A lightweight client, also known as a simplified-payment-verification (SPV) client, connects to a full node or other remote server for receiving and sending Bitcoin transaction information, but stores the user wallet locally, partially validates the transactions it receives, and independently creates outgoing transactions.

###### Third-party API client

A third-party API client is one that interacts with Bitcoin through a third-party system of APIs rather than by connecting to the Bitcoin network directly. The wallet may be stored by the user or by third-party servers, but the client trusts the remote server to provide it with accurate information and protect its privacy.
