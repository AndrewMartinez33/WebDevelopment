# SSH

## SSH or Secure Shell is a protocol.

- Allows users to share files and modify or control computers over the internet
- All data is encrypted
- Can talk to the operating system

## Symmetrical Encryption

- has 1 key that encrypts and decrypts the data
- anyone that has the key can decrypt the message

## Asymmetrical Encryption

Assymentrical encryption uses public-private key pairs to encrypt and decrypt data. Suppose you have two users:

Alice and Bob both have a pair of private and public keys. When they want to send a message to eachother, they would exchange public keys. Alice will use Bob's public key to encrypt a message and send it to Bob. Since the message is encrypted with his own public key, the only way to decrypt it is with Bob's private key. And vice versa, if Bob wants to send a message to Alice he will encrypt the message with Alice's public key.

- the public-private keys are linked together and have a one way relationship. The public key can encrypt a message, but can never decrypt the message.
- the private key should NEVER be shared.
- the initial exchange of public keys is done using the Diffie Hellman Key Exchange algorithm

## Diffie Hellman Key Exchange

add diffie hellman info

## Hashing

Another form of cryptography. They generate a unique value and are one way. They cannot be decrypted. If one thing is changed in the message, they unique value will be completely different. When can use this to prevent man in the middle attacks. If someone tampers with the message, the hash number will change.
