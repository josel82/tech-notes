# Cryptography

## Hashing
Used for message integrity
```
echo -n "Hello" | md5sum
```

```
md5sum myFile.txt
```

by default, the echo command add a line break after the word, the `-n` flag removes that line break.

### Hashing Algorithms

| Algorithm    | Length   | Command   |
| ------------ | -------- | --------- |
| MD5          | 128 bits | md5sum    |
| SHA/SHA1     | 160 bits | sha1sum   |
| SHA2 Family: |          |           |
| SHA-224      | 224 bits | sha224sum |
| SHA-256      | 256 bits | sha256sum |
| SHA-384      | 384 bits | sha384sum |
| SHA-512      | 512 bits | sha512sum |

### MAC (Message authentication code)
keyed hash function used to protect a message's integrity and authenticity

#### Types of MACs:

- **HMAC (Hash-based Message Authentication Code)**: Combines a cryptographic hash function (e.g., SHA-256) with a secret key.
- **CMAC (Cipher-based Message Authentication Code)**: Uses a block cipher (e.g., AES) and an initialisation vector (IV).
- **KMAC (Keyed-Hash Message Authentication Code)**: A variant of HMAC using a keyed hash function.



## Encryption

### Asymmetric Encryption Algorithms
Restricted to limited data (CPU intensive).
Don't require key exchange.

- DSA (Less secure)
- RSA (Secure) - Recommended key size 2048 bits
- Diffie-Hellman (Secure)
- ECDSA (Secure)
- ECDH (Secure)

### Symmetric Encryption Algorithms
Ideal for bulk data (easy on the CPU).
Require key exchange.

- DES (Insecure) - 56 bit key
- RC4 (Insecure) - 128 bit key
- 3DES (Less secure) - 168 bit key
- AES (Secure) - 128, 192, or 256 bit keys
- ChaCha20 (Secure) - 128 or 256 bit keys