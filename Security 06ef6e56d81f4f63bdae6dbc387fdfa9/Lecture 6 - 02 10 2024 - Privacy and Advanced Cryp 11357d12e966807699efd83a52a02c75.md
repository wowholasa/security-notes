# Lecture 6 - 02.10.2024 - Privacy and Advanced Cryptography

# Birth of Modern Cryptography

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image.png)

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%201.png)

# A Practical (Legal) Motivation: GDPR and Personal Data

- EU’s General Data Protection Regulation
- Data Processors must obtain consent from subjects before processing their data and inform of how data will be used
- Data subjects also have rights to: erasure, access, rectification, restrict processing, portability, object to processing
- Data subjects have special personal data: race/ethnicity, political opinion, religious beliefs, sexual life/orientation, health/genetic idea
- 

# A Practical (Legal) Motivation: Schrems II

- Decision by the Court of Justice of the European Union in 2020
- European companies acting as data controller or processors use cloud services from US-based companies (e.g. AWS, Azure, Google).
- “Standard Contract Clauses” (SCCs) in contracts with US-based cloud service providers state that they will comply to GDPR (e.g. data stays in the EU).
- There is evidence that US-based cloud service providers can be forced to transfer data to the US, where they are subject to US law. (Clear breach of GDPR)
    - US companies bad.
- European data controllers and processors must now make sure that their costumer data processed by US-based cloud service providers will abide by the GDPR.

General understanding (In Denmark) is that if the data is encrypted, then it’s fine, HOWEVER:

US services might not just store data, but process it. If the services are running on US cloud services that might be a problem.

# Secure Multi-Party Computation (MPC)

- Parter $P_1, ..., P_n$ vil gerne compute funktion $f(x_1,...,x_n)$
- De følger en protokol der sender beskeder over netværket indtil de får $y=f(x_1,...,x_n)$
    - Antallet af beskeder der bliver sendt kan afhænge af antallet af parter og/eller funktion

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%202.png)

## Adversarial Model

- Honest parties: Følger altid protokollen!
    - Prøver ikke at ændre output, eller gøre noget for at lære andres private inputs.
- Formelt er der én adversary, der corrupter gruppen
- Corrupted parties: Er kontrolleret af adversary.

Fordi vi har ordentlige protokoller på vores netværk, opfører man sig ikke længere som en Dolev-Yao adversary - Istedet hacker man devices.

### Adversarial Models: Adversary Types

- Honest But Curious (or Passive) Adversaries: Don’t deviate from the protocol but try to break its security by observing messages.
- Malicious (or Active) Adversaries: deviate from the protocol, see in party’s memory , change memory, send out messages that don’t follow protocol
- Covert adversaries: deviate from the protocol if it is profitable from them (they don’t want to get caught)

### Adversarial Models: Static vs Adaptive

- Static adv: corrupts all parties before protocol execution starts
    - Sker normalt ikke i den virkelige verden.
- Adaptive adv: corrupts all parties at any point before or after protocol execution starts.

Compromise often occurs from human error or software bugs.

Adversary will eventually get into our devices - What do we do when we cannot trust that our devices are safe and will keep our data secure?

- Secure Multiparty communication can help withstand this issue.

## Applications

- Auctions: e.g. the annual Danish sugar beats auction.
    - MPC used to replace consulting companies.
- Distributed randomness generation: e.g. lotteries/games/blockchains
- Financial benchmarking: e.g. helping banks decide how to give loans without learning people’s private financial data
- Privacy preserving supply chains
- Avoiding Satellite collisions
- Any kind of privacy preserving computation on sensitive data.

## MPC Question

In a MPC computation of a function $f(x_1,…,x_n)=x_1+…+x_n$ where party $P_i$ has an input bit $x_i$  for $i=1,…,n$, what statement is correct?

1.  The adversary learns nothing about the honest party inputs.
2. The adversary can make the protocol output an arbitrary value.
3. The adversary only learns the output but not the individual inputs.
    1. Korrekt.
4. The parties compute the output locally.

# t-out-of-n Threshold Secret Sharing

- Stærkere end encryption
- Afhænger ikke af at adversary er computationally restrained, eller særlig avancerede udregniner
- Perfekt secrecy
- t er treshold, hvis adversary kender t  shares kan de ikke lære noget om vores secret.
- Hvis du får nok shares, kan du rekonstruere den originale secret.

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%203.png)

## A Simple n-out-of-n Additive Secret Sharing

- Sharing a secret s from $ℤ^*_p$ using addition modulo p:
    - Sample n-1 random shares $s_1,…, s_{n-1}$ from $ℤ^*_p$.
    - Compute $s_n = s-(s_1+…+ s_{n-1} ) \mod p$, where s is the secret.
    - The final shares vector is $(s_1,…, s_n)$.
- Clearly, the secret s can only be obtained if all shares (s1,…, sn) are known. Otherwise, the one missing shares acts as a one-time pad, hiding the secret perfectly.
- BONUS: you can add secrets privately by adding their shares!

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%204.png)

## Commitments

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%205.png)

- Det er ikke encryption selvom det ligner.  Der er ingen nøgle til at decrypte

### Hash Based Commitments

- Use a cryptographically secure Hash Function H:{0,1}*->{0,1}^k
- Computing a commitment Com(m,r): Alice samples a random k-bit
string r and computes c=Com(m,r)=H(r|m), concatenating r and m.
    - Hiding: intuitively it is hard to invert a hash function or find a preimage, so when Alice sends c to Bob, he cannot find r|m that were used to compute m.
    - Using randomness r is important, otherwise if m is predictable, Bob can bruteforce many different m until finding H(m)=c.
- Opening a commitment: Alice sends r|m to Bob, who tests c=?H(r|m)
    - Binding: intuitively it is hard to find a collision r’|m’ != r|m such that H(r|m)=H(r’|m’), so Alice cannot lie about the original r|m to Bob.

### Pedersen commitments

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%206.png)

## Coin Tossing

- Alice and Bob want to generate a random bit such that none of them can predict (or influence) what the bit will be.
- Coin Tossing protocol by Blum:
    1. Alice samples random bit a and sends commitment Com(a,r) to Bob.
    2. Bob samples a random bit b and sends it to Alice.
    3. Alice sends (a,r) to Bob, who checks that it is a valid opening for Com(a,r).
    Both Alice and Bob compute the output as a XOR b.
- Bob does not know Alice’s bit a, so he cannot influence the output.
- Alice cannot change her bit a after seeing Bob’s bit b, so she also cannot influence the output.

## Summary

- Cryptography can be used to compute on private data without
revealing it, it can be done with many different security guarantees.
- We use protocols with many parties and consider adversaries can
corrupt them gaining complete control and learning their data.
- Simple computations like generating a random bit can be done
efficiently using commitments, which can be built from different
primitives like hash functions or from problems like discrete log.
- Secret sharing allows us to split a secret into many shares that don’t
reveal anything about the secret, it can be used to do secure
multiparty computation.

# Bitcoin and Blockchains zzzz

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%207.png)

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%208.png)

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%209.png)

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%2010.png)

Consensus: 

- Byzantine agreement: Byzantine generals problem

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%2011.png)

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%2012.png)

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%2013.png)

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%2014.png)

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%2015.png)

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%2016.png)

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%2017.png)

![image.png](Lecture%206%20-%2002%2010%202024%20-%20Privacy%20and%20Advanced%20Cryp%2011357d12e966807699efd83a52a02c75/image%2018.png)