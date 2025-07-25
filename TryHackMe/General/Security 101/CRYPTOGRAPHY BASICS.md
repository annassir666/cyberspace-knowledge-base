#thm #fundamentals #cryptography

---

Cryptography's ultimate purpose is to ensure a `secure communication` in the presence of adversaries. The term 'secure' includes confidentiality and integrity of the communicated data.

Cryptography is used to protect confidentiality, integrity, and authenticity.

There is a variety of different standards to protect and handle information. 
- PCI DSS - for banking systems. 
- HIPAA (Health Insurance Portability and Accountability Act)
- HITECH (Health Information Technology for Economic and Clinical Health) in the USA


Everything from text to photo or video is a plaintext in terms of cybersecurity. They are original and readable information. To protect this data, we use `encryption`, which turns plaintext into a `ciphertext`. This process uses a key and encryption function, which together make up a `cipher` - a set of rules to convert a plaintext into cipher-text and vise versa.

- **Plaintext** is readable data before encryption.  
- **Cipher-text** is the scrambled, unreadable form after encryption.  
- **Cipher** is the algorithm that transforms plaintext to cipher-text and back.  
- **Key** is a secret string of bits used by the cipher to encrypt or decrypt data.  
- **Encryption** turns plaintext into cipher-text using a cipher and key.  
- **Decryption** reverses encryption, turning cipher-text back into plaintext with the key.


## Types of Encryption
The two main categories of encryption are **symmetric** and **asymmetric**.

### Symmetric encryption
`Symmetric encryption or Symmetric cryptography` uses the same key to encrypt and decrypt data. Keeping the key secret is a must; it is also called **private key cryptography**.
It is risky to transfer to key to the receiver without a secured channel.

Examples of symmetric encryption:

- **DES (Data Encryption Standard)**
    - Adopted in 1977 with a 56-bit key.
    - Broken in under 24 hours by 1999 due to advances in computing.
    
- **3DES (Triple DES)**
    - Applies DES three times, resulting in a 168-bit key (112-bit effective security).
    - Introduced as a temporary fix when DES became insecure.
    - Deprecated in 2019 but still used in some legacy systems.
    
- **AES (Advanced Encryption Standard)**
    - Adopted in 2001 as the modern standard.
    - Supports key sizes of 128, 192, or 256 bits.


## Asymmetric Encryption

`Assymetric Encryption` uses to different keys: one to encrypt and the second to decrypt. To protect confidentiality, asymmetric encryption uses the public key to encrypt.

Examples are RSA and ECC.

Asymmetric encryption is based on a particular group of mathematical problems that are easy to compute in one direction but extremely difficult to reverse. In this context, extremely difficult means practically infeasible

---

## Basic Math

- XOR Operation
- Modulo Operation

### XOR Operation

XOR, short for “exclusive OR”, is a logical operation in binary arithmetic that plays a crucial role in various computing and cryptographic applications. In binary, XOR compares two bits and returns 1 if the bits are different and 0 if they are the same.

This operation is often represented by the symbol ⊕ or ^.

| A   | B   | A ⊕ B |
| --- | --- | ----- |
| 0   | 0   | 0     |
| 0   | 1   | 1     |
| 1   | 0   | 1     |
| 1   | 1   | 0     |

A truth table shows all possible outcomes of a logic operation. For the XOR (⊕) operation, the results are: 0 ⊕ 0 = 0, 0 ⊕ 1 = 1, 1 ⊕ 0 = 1, and 1 ⊕ 1 = 0. For example, if we XOR the binary numbers 1010 and 1100 bit by bit, we get 0110, since 1 ⊕ 1 = 0, 0 ⊕ 1 = 1, 1 ⊕ 0 = 1, and 0 ⊕ 0 = 0. XOR is useful in cryptography due to its key properties: XORing a value with itself gives 0 (A ⊕ A = 0), and XORing a value with 0 leaves it unchanged (A ⊕ 0 = A). It is also commutative (A ⊕ B = B ⊕ A) and associative ((A ⊕ B) ⊕ C = A ⊕ (B ⊕ C)). These properties allow XOR to be used for simple symmetric encryption. If P is the plaintext and K is the key, the ciphertext is C = P ⊕ K. To decrypt, we compute C ⊕ K, which simplifies back to P. This works because (P ⊕ K) ⊕ K = P ⊕ (K ⊕ K) = P ⊕ 0 = P. In practice, secure use requires the key to be as long as the message.


### Modulo Operation

The modulo operator (written as `%` or `mod`) gives the remainder after dividing one number by another. For example:

- `25 % 5 = 0` because 25 ÷ 5 = 5 with no remainder
    
- `23 % 6 = 5` because 23 ÷ 6 = 3 with a remainder of 5
    
- `23 % 7 = 2` because 23 ÷ 7 = 3 with a remainder of 2
    

In everyday math, we often ignore the remainder, but in cryptography, it’s very important.

Modulo is not reversible. For example, many numbers satisfy `x % 5 = 4` (like 4, 9, 14, etc.).

When using large numbers in cryptography, calculators might not work well. Programming languages like Python can handle big integers easily. Online tools like WolframAlpha can also help.

A key rule: `a % n` always gives a result from 0 to `n - 1`.