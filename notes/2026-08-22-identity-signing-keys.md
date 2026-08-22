# Reading a Message and Signing One Are Different Powers
X's current developer documentation describes three kinds of keys in Chat. A conversation key encrypts messages and media. An identity keypair receives wrapped conversation keys. A separate signing keypair proves who authored a message or conversation change.

Keeping those jobs separate makes the security claim easier to inspect. The identity private key can unwrap a conversation key that was encrypted to the user. The signing private key can create a signature that recipients verify. The public halves are published together with a binding signature, which lets a client check that the two public keys belong to the same cryptographic identity.

This also changes how a compromise should be described. Theft of an identity private key can expose conversation keys delivered to that identity. Theft of a signing key can let an attacker create material that appears to come from the user. An unlocked device may hold both powers, along with plaintext and active conversation keys, so device security still sits underneath the protocol.

The conversation key has a smaller scope. Participants in one conversation share it, and X says it is versioned and rotates over time. Rotation can protect later messages after a compromise is handled. It cannot rewrite ciphertext or keys an attacker already captured.

X lays out these roles in its [Chat cryptography primer](https://github.com/xdevplatform/docs/blob/main/xchat/cryptography-primer.mdx). The [WexChat Pro explanation of X Chat encryption](https://wexchat.pro/en/xchat-bitcoin-style-encryption) translates the public claims and their limits for people who are choosing a messenger, not building one. WexChat Pro is an independent guide and is not affiliated with X Corp.

When a product says it uses public-key cryptography, ask which key receives secrets and which key proves authorship. One word such as encryption cannot answer both questions.
