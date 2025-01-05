# Lecture 12 - Post Quantum Cryptography

# Part 1: Quantum Computing - Opportunities and threats

## Outline Part 1

- Quantum computers
- Opportunities
    - Quantum algorithm for quantum chemistry
- Threats
    - Which cryptographic algorithms are vulnerable?
    - Where are they used=
    - How does a quantum computer break cryptographic algorithms? (Cartoon-level…)

## Quantum computers - What is a quantum computer?

Computing based on quantum mechanical effects.

Quantum physics is used for processing “non-quantum” information

It is used in information technology:

- Semiconductors
    - Transistors
    - Flash memory
    - OLED
    - …
- Optical communication
- 3D movie theatre
- …

> Information is Physical
- Rolf Landauer
> 

⇒ If the physics is quantum, information is as well!

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image.png)

So what is a quantum computer?

Short answer:  We don’t really know yet!

### Qubit platforms

A qubit is the basic unit of information in quantum computing.

In theory we could use quantum computers for these applications:

- Superconducting
- Photonic
- Cold atoms
- Trapped ions

They are however not stable enough and produce too many errors.

### Potential applications of quantum computing

- Quantum chemistry simulation (For material science, pharmacology, battery tech…) (GOOD)
- Breaking cryptographic schemes (BAD)
- Optimization?

# Opportunities

## Chemistry

Pharmacology, battery technology, fertilizer production, synthetic fuels….

Currently the process of innovation is very expensive and can take potentially forever.

You need to keep testing and experimenting.

With a quantum computer it would be faster and cheaper to simulate it!

### Computational chemistry

Huge field of research and development

- Countless methods of approximaiton, simulation etc. for different regimes
- When is it feasible?
    - Only with small molecules, not very big molecules

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%201.png)

### Why can’t we simulate chemistry?

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%202.png)

### Quantum algorithms for chemistry

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%203.png)

# Threats - Which cryptographic algorithms are quantum-vulnerable?

- RSA
- Diffie-Hellman (ordinary and elliptic curve)

⇒ All* currently used public-key crypto!

## Where are the broken schemes?

Answer: Essentually everywhere

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%204.png)

Definitely whenever:

1. A new secure connection is established; or
2. Something is publicly verifiable

## Example TLS - Quantum vulnerabilities in TLS

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%205.png)

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%206.png)

DH problem and RSA problem just break

⇒ both building blocks of Handshake break

## Example RSA

- Public-key cryptosystem: encryption and digital signature
- Based on number theory
- Used e.g. in HTTPS, Certificates…
- Can be broken via factoring

### Factoring

- Multiplying is easy
- Factoring is hard!

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%207.png)

- In RSA: Factors are private key, product is the public key

Factoring is hard, BUT it is **not hard for quantum computers**!

## Assessing quantum attack risk

**By when do we need to fix quantum-vulnerabilities?**

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%208.png)

- How big is *y*? Example: WEP to WPA transition
- Ho big is *x*? Depends on the application. Example: Data covered by GDPR? Seems reasonable to set *x*=human life span
- How big is *z*? Hard to say…

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%209.png)

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%2010.png)

## Summary: quantum computing threat

- Quantum computers are fundamentally different from regular computers
- Quantum computers are currently not available
- Time horizon according to experts: ~15-30 years
- They have a computing power incomparable to regular computers
- They are good at discovering structure in big mathematical objects
- They can be used to launch attacks against RSA and Diffie-Hellman
- Important: Be aware of Risk timeline

# Interlude: Hype

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%2011.png)

# Part 2: Post-quantum public-key cryptography

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%2012.png)

Luckily, public-key encryption and key exchange can also be constructed based on the hardness of 

- Lattice problems
- Solving systems of multivariate polynomial equations
- Decoding “obfuscated” error correction codes
- Finding an isogeny between supersingular elliptic curvers

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%2013.png)

## Post-quantum cryptography

⇒ We have

- Lattice-based
- Multivariate-polynomial-based
- Code-based
- Isogeny-based

Public-key encryption/key exchange

Digital signatures are “easier”! Additionally

- Hash-based signatures
- MPC-in-the-head signatures

Standardized stateful post-quantum signature schemes are available:

XMSS (Hash-based)

However: signatures less time-critical

## NIST post-quantum crypto standardization

- Goal: Standardize at least one PQ-secure scheme of each:
    - Key Encapsulation Mechanism (KEM, ~public-key encryption)
    - Digital Signature scheme (DSS)
- Initially: All classes represented (Lattice, code, multiv. polynomial,
isogeny)
- To be standardized (probably 2024):
    - 1 Lattice KEM: Crystals-Kyber (draft standard just published)
    - 3 DSS: 2 based on lattices: Crystals-Dilithium&Falcon, 1 hash-based:
    SPHICS+ (draft standard just published, except Falcon)
- 4th round: New call for signature proposals (~40 submissions), 3 codebased KEMs under consideration

## Kyber

Scrutinized by international community of experts for years

- Seems secure
- But how about performance?
    - 

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%2014.png)

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%2015.png)

Basically no increase in delay!

### Quantum vulnerabilities in TLS - Fixed with Kyber?

![image.png](Lecture%2012%20-%20Post%20Quantum%20Cryptography%2014457d12e966803aa23cec5abf0bc4f7/image%2016.png)

The solution to quantum threats is not more quantum. 

It is perfectly normal cryptography.

### How does Kyber work?