#bitcoin #bitcoin-book 

The original Bitcoin paper describes a very simple scheme to make a transaction.

- A receiver accepts bitcoins using a **public key**.
- A sender uses it's **private key** to sign the transaction.

## Public key Cryptography
#cryptography
Public key cryptography was invented in the 1970s and is a mathematical foundation for modern computer and information security.

Public key uses **mathematical functions** that are easy to calculate in one direction and infeasible to calculate in the opposite direction (using the computer and algorithms available today).

- Bitcoin uses the **elliptic curve addition** and **multiplication** as the basis for its cryptography.
- In Bitcoin we can create a public and a private key using cryptography.
- These keys are used to controls access to bitcoins.
- The keys pair consists of a private key and a public key **derived from the private key.
- The **public key** is used to **receive bitcoin**.
- The **private key** is used to **sign transactions** to send bitcoins. 
- There is a **mathematical relationship** between the public and private key.
- The **relationship** between the keys allows the private key to **generate signatures** and this signatures can be **validated** against the public key.
- This allow signatures to be verified without reveling the private key.
- The private key (k) is a number, usually derived from a number picked at **random**.
- From the private key (k) its used **elliptic curve multiplication** to generate a **public key** (K)
- Anyone with access to the public key an the transaction can **verify the signature**. 

## Private Keys

- Control over the private key is control over **all funds** associated with the corresponding Bitcoin public key.
- The private key used to sign transactions, **proving control** of the funds.
- The private key must remain secret at all times.
- The private key must also be backed up and protected from accidental loss. If you loss it you lose control over all the funds secured by it.

### Generating a Private Key

- A private key is just a number.
- Be careful, as any process that's less than **completely random** can significantly reduce the security of your private key.
- Computer scientists call this randomness **entropy**.
- More precisely, the private key can be any number between 0 and _n_ - 1 inclusive, where _n_ is a constant (_n_ = 1.1578 × 1077, slightly less than 2256) defined as the order of the elliptic curve used in Bitcoin.

**Private key**:
(256 bits shown as 64 hexadecimal digits, each 4 bits)
```
1E99423A4ED27608A15A2616A2B0E9E52CED330AC530EDCC32C8FFC6A526AEDD
```

## Elliptic Curve Cryptography Explained
#ECC

	This section is a bit confusing to me.
	I think I lack a deeper knowledge of mathematics.

Elliptic curve cryptography (ECC) is a type of asymmetric or public key cryptography based on the discrete logarithm problem as expressed by addition and multiplication on the points of an elliptic curve.

Bitcoin uses a specific elliptic curve and set of mathematical constants, as defined in a standard called **secp256k1**. 

The secp256k1 curve is defined by the following function, which produces an elliptic curve:

$$
\begin{equation}
{y^2 = (x^3 + 7)}~\text{over}~(\mathbb{F}_p)
\end{equation}
$$

- Given two points `P1`e `P2` on the elliptic curve, there is a third point `P3 = P1 + P2`, also on the elliptic curve.

Using the same strategy as the property above they create public keys. They multiply a point `G` for the **private key** and it generates the **public key**. So the public key is also a point on the elliptic curve.

$$
P_{3} = P_{1} + P_{2} 
$$
$$
K = k \times G = G+G+\dots+G (k\ times)
$$
Just think that `P3` is `K` and `P1` and `P2` are the same number: `G`.

## Public Keys

The public key is calculated from the private key using **elliptic curve multiplication**, which is irreversible:
$$
K = k \times G
$$
Where `k` is the **private key**, `G` is a constant point called the **generator point**, and `K` is the resulting **public key**.

The reverse operation, Know as `"Finding the discrete logarithm"` (calculate `k` if you know `K`) is as difficult as trying all possibilities of `k`.

- The **generator point** `G` is the **same for all keys** in bitcoin.
- A **private key** can be converted into a **public key**, but a public key **cannot** be converted into a private key.

**Private key is defined as a point**:
$$
K = (x,y)
$$
```
x = F028892BAD7ED57D2FB57BF33081D5CFCF6F9ED3D3D7F159C2E2FFF579DC341A
y = 07CF33DA18BD734C600B96A72BBC4749D5141C90EC8AC328AE52DDFE2E505BDB
```

To visualize multiplication of a point with an integer, we will use the simpler elliptic curve over real numbers—remember, the math is the same. Our goal is to find the multiple _kG_ of the generator point _G_, which is the same as adding _G_ to itself, _k_ times in a row. In elliptic curves, adding a point to itself is the equivalent of drawing a tangent line on the point and finding where it intersects the curve again, then reflecting that point on the x-axis.

#### OBS

Many Bitcoin implementations use `libsecp256k1` cryptography library to do the elliptic curve math.

## Output and Input Scripts

