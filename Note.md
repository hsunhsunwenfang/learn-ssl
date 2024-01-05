

# cryptography for computer security

https://opensource.com/article/18/5/cryptography-pki

- Attribute of secure communication
    - confidentiality
        - a message is only readable by the sender and the receiver
    - integrity
        - a message cannot be modified in transit
    - Authentication
        - a message can be verified to have been sent by a particular person

- Cipher
    - Encrytable and Decryptable
        - XOR can be used in a one-time pad
    - One-time pad
        - a key that is as long as the message itself
        - the key is used only once
        - the key is truly random
        - the key is never reused
        - the key is kept secret
    - But, it is not practical
        - Secure key exchange is difficult
        - Random number generators are not truly random
        - Large keys are difficult to manage
    - Symmetric Cipher
        - A single key is used for both encryption and decryption
        - One key for one receiver -> too many keys to manage
        - Is slower so we shorten message by hashing it before encryption
        - Stream ciphers
            - Runs the key through a pseudo-random number generator one byte at a time
            - XORs the output of the pseudo-random number generator with the plaintext
            - Useful when the length of the message is unknown
            - RC4 -> vulnerable to attacks like the Fluhrer, Mantin and Shamir attack -> TLS 1.3 no longer supports RC4
        - Block ciphers
            - fixed-length blocks of plaintext are encrypted under the same key
            - AES (Advanced Encryption Standard) -> 128-bit blocks
                - mode -> describes how to encrypt arbitrary-length messages
            - ECB (Electronic Code Book)
                - simplest mode -> each block is encrypted independently
                - But reveals patterns in the plaintext
            - CBC (Cipher Block Chaining)
                - each block is XORed with the previous ciphertext block before being encrypted
                - the first block is XORed with an initialization vector (IV)
                - the IV is transmitted in the clear, so it must be random, unique, and unpredictable
    - Asymmetric Cipher
        - private key for decryption and public key for encryption
        - computationally expensive
        - RSA
    - Used together
        - Asymmetric cipher for key exchange
        - Symmetric cipher for bulk encryption

- Random Number
    - Gather entropy from the environment
        - mouse movements, keyboard timings, network traffic, disk timings, etc.
        - time consuming and cannot ensure the quality of the entropy

- Cryptographic hash function
    - A one-way function
        - easy to compute the hash of a message
        - computationally infeasible to find a message that hashes to a given value
    - Collision resistance
        - computationally infeasible to find two messages that hash to the same value
    - MD5
        - 128-bit hash value
        - broken
    - SHA-1, SHA-2, SHA-3
        - SHA-1 -> 160-bit hash value
        - SHA-2 -> 224, 256, 384, or 512-bit hash value
        - SHA-3 -> 224, 256, 384, or 512-bit hash value
    - HMAC (Hash-based Message Authentication Code)
        - H(K XOR opad, H(K XOR ipad, text))

- Complete Picture
    - https://en.wikipedia.org/wiki/Hybrid_cryptosystem
    - Parties
        - S : Sender, R : Receiver, K : Key
    - S picks a random symmetric key
    - S encrypts the symmetric key with the R's public key
    - S hashes the message
    - S signs the hash with S's private key
    - R receives the signature and the signed hash
    - R compares the hash of the signed hash with the hash in the signature
        - If match, the integrity and authenticity of the message are verified
    - R decrypts the symmetric key with R's private key
    - Communication goes on with the symmetric key of HMAC

# openssl

https://opensource.com/article/19/6/cryptography-basics-openssl-part-1

- SSL with c++




# TLS, SSL, CA

https://opensource.com/article/19/11/internet-security-tls-ssl-certificate-authority


