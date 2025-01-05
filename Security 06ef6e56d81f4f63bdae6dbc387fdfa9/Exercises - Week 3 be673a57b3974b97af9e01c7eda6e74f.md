# Exercises - Week 3

# Review Questions

## 2.1 How is cryptanalysis different from brute-force attack?

Cryptanalysis requires you to apply some logic and not just brute force. 
For example that could be pattern analysis or analysing the frequency of the letters.

## 2.5 What is one-way hash function?

En funktion der tager en besked og returnerer en fixed-size hash 

# Problems

## 2.1 Typically, in practice, the length of the message is greater than the block size of the encryption algorithm. The simplest approach to handle such encryption is known as electronic codebook (ECB) mode. Explain this mode. Mention a scenario where it cannot be applied. Explain briefly why it is not a secure mode of encryption.

Plaintext → Block cipher encryption with a key → Ciphertext

Disadvantage: Lack of diffusion

## 2.6 Suppose H(M) is a cryptographic hash function that maps a message of an arbitrary bit length on to an n-bit hash value. Briefly explain the primary security requirements of the hash function H. Assume that H outputs 16-bit hash values. How many random messages would be required to find two different messages M and M' such that H(M) = H(M′).

Requirements:

- **Preimage Resistance**: Given a hash value h=H(M)h = H(M)h=H(M), it should be computationally infeasible to find the original message MMM such that H(M)=hH(M) = hH(M)=h.
- **Second Preimage Resistance**: Given a message MMM and its hash H(M)H(M)H(M), it should be computationally infeasible to find another message M′M'M′ such that H(M)=H(M′)H(M) = H(M')H(M)=H(M′) (i.e., no two different messages should have the same hash).
- **Collision Resistance**: It should be computationally infeasible to find any two different messages MMM and M′M'M′ such that H(M)=H(M′)H(M) = H(M')H(M)=H(M′). This ensures that no two different inputs result in the same hash output.

Outputs:

- Since the hash function produces a 16-bit output, there are 216=65,5362^{16} = 65,536216=65,536 possible distinct hash values.
- According to the **birthday paradox**, the number of random messages needed to find a collision (two messages MMM and M′M'M′ such that H(M)=H(M′)H(M) = H(M')H(M)=H(M′)) is approximately 2n\sqrt{2^n}2n​, where nnn is the number of bits in the hash output.

For a 16-bit hash value:

![image.png](Exercises%20-%20Week%203%20be673a57b3974b97af9e01c7eda6e74f/image.png)

Thus, **approximately 256 random messages** would be required to find a collision using the birthday attack.