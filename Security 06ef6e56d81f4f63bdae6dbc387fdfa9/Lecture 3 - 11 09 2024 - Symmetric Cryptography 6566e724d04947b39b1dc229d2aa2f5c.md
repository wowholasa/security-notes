# Lecture 3 - 11.09.2024 - Symmetric Cryptography

# Review

- Cyclic Groups (Revise for next lecture)
- Attacks on the network stack: no confidentiality and integrity
- Denial of service attacks

# Motivation

- Protect data confidentiality, integrity and availability on insecure networks
- Based on strong mathematical foundations: proven to be secure instead of conjectured
- We use cryptography every day to access web sites and services securely

# Symmetric Encryption (confidentiality)

## Fundamentals

- Videnskaben af at transformere en given string til en forskellig string der er semantisk ekvivalent (encryption), fordi den anden string kan transformeres tilbage til den originale (decryption)

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image.png)

# Symmetric Cryptography (confidentiality)

**Definition:** The same key as the one that was used to create a ciphertext by encrypting a plaintext shall be used to decrypt the ciphertext back as the plaintext

**Goal:** confidentiality

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%201.png)

Eksempler: 

- Caesar’s cipher, DES, 3DES, AES
- Typical length: 128/256 bits
- Good performance

## Caesar cipher

Caesar cipher fungerer ved at alfabetet bare er “shifted” et par gange.

k = key 

c = cipher

m = message

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%202.png)

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%203.png)

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%204.png)

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%205.png)

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%206.png)

## Mono-alphabetic substitution

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%207.png)

Brute force bliver sværere en Caesar Cipher

Hvis vi kender sproget beskeden er skrevt på, så ved vi hvad average frequency er på forskellige bogstaver i original sproget, så i den enkrypterede besked er frequency vedligeholdt.

## Perfect Secrecy

- Vernam cipher or One-time pad
- Idea: use the properties of XOR to encrypt and decrypt

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%208.png)

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%209.png)

- At kende ciphertexten fortæller dig intet om original beskeden
    - For hver ciphertext eksistere der en key der mapper til en hver plaintext

- Problem 1: Key length = message length
    - Encryption af en 500GB hard drive ville kræve 500GB RAM
- Problem 2: Nøglen kan kun bruges én gang

## Block Cipher

Problem 1: Key length = message length 

- Idea: agree on a short key and generate fixed-length permutations from the key

Problem 2: the key can only be used once

- Idea: use a random value on each encryption (aka initialisation vector)

Multiple variants of block cipher exists

### Cipher Block Chaining

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2010.png)

### Cipher

Security: A (block) cipher is secure if it is a good *pseudorandom permutation function*

**Pseudorandom permutation (Very informal)**

- The output of a of a secure cipher cannot be distinguished from a random permutation

### Confusion

Make the connection between ciphertext and key as complicated as possible

### Diffusion

Flipping a single bit of the plaintext (statistically) produces a flipping of half the bits in the ciphertext

## AES

Asymmetric Encryption Standard

- State-of-the-art symmetric encryption algorithm

Block length = 128 bits

- messages that are not multiple of block length are padded

Key length = 128, 192 or 256 bits

Number of rounds = 10, 12, or 14

- Each round consists of layers

NSA classifies as TOP SECRET AES192 and AES256

- Not practical attack known on AES, when correctly implemented

**We focus on AES128**

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2011.png)

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2012.png)

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2013.png)

### AES - Byte Substitution layer (S-Box)

- En S-box har følgende properties:
    - **Identical** dvs. samme s-boxes per runde
    - **Nonlinear** dvs. $S(s)+S(s') \neq S(s+s')$
    - **Bijective** dvs. $\exists_1$ 1-to-1 mapping af input og output bytes
        - S-box can be uniquely reversed
    - Implementeret som en lookup table

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2014.png)

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2015.png)

### AES - Diffusion Layer

**Diffusion** over alle input state bits

- ShiftRows giver permutation af dataen
- **Linear** dvs $ShiftRows(s)+ShiftRows(s') = ShiftRows(s+s')$
    - Lignende gælder MixCols
- MixCols giver mix af block af 4 bytes

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2016.png)

### AES - Key Addition Layer

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2017.png)

### AES - Roundup

- **S-boxes** giver **confusion**
- **ShiftRows** og **MixCols** giver **diffusion**
- **Key Addition Layer**beskytter **mod inverting angreb**

AES anses som sikker fordi:

- *conjectured *****for at være en god **pseudorandom permutation** funktion
- Har ingen *særiøs ***cryptoanalysis** angreb indtil videre

# Hash and MAC (integrity)

## Hash functions

Almen byggeblok af sikkeheds mekanismer:

- Sammenlign med hash
- Virus beskyttelse
- OTP
- holde kodeord
- fundamental ingrediens for mange crypto primitiver

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2018.png)

## Cryptographic Hash functions

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2019.png)

## Hash functions: Application (Kommer til at blive dækket i Authentication forelæsningen)

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2020.png)

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2021.png)

NEJ - For 3. og 5. password er det samme og har samme hash…

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2022.png)

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2023.png)

## Message Authentication Codes (MAC)

Goal: integrity + authenticity

- Ikke confidentiality!

En **algoritme** tag = mac(m, k)

En **algoritme** d = ver(tag,m,k)

- k = KeyGen() som er en tilfældig string
- k skal være hemmelig!!!

Correctness: ver(mac(m,k),m,k) = true

## HMAC

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2024.png)

*insert slides der ikke er i de uploadede slides senere*

## MAC Application

![image.png](Lecture%203%20-%2011%2009%202024%20-%20Symmetric%20Cryptography%206566e724d04947b39b1dc229d2aa2f5c/image%2025.png)

## Limitations of symmetric cryptography

- Sender og Receiver skal mødes **in person** og vælge k (key)
- Skal bruge en key **for hver par af agenter** der vil kommunikere sikkert (DET ER RIGTIG MANGE KEYS)
- *insert 3. punkt senere når slides er odpateret*