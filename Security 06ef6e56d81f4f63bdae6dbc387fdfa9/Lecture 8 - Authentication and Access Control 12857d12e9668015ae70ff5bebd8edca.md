# Lecture 8 - Authentication and Access Control

# Authentication

### Security Goals

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image.png)

Bruges til at bevise vi er de brugere, vi påstår vi er. 

### Definition

Verify claim of identity

### Examples

Authenticaton of a server (TLS/Certificates), an identity (e-passport), a human being (captcha), etc.

## Factors

**Knowledge -** Something you know: Password, PIN, key, etc…

**Possession -** Something you have: smartcard, smart token, passport

**Inherence -** Something you are: fingerprint, iris, typing dynamics

The best approach is always to use more than one factor!

## Knowledge-based Authentication

Måder knowledge-based authentication kan fejle:

- En adversary kan gætte dit password, hvis de kender noget om dig.
- De kan stå bag dig (overvåge dig) og se dit password.
- Spoofing
- Sniffing - I dag er det sværere at gøre, pga. TLS. Men basically at der eavesdroppes på det du sender over serveren.
- Server breach - stjæler ikke blot dit password, men alles womp womp

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%201.png)

### Guessing

Klassisk angreb:

- Kort, forudsigeligt, bruger-relateret password (e.g. molly1234)

Dictionary attack:

- Prøv alle ord fra en liste

Bruteforce attack:

- Prøv alle karaktere fra et givent charset (e.g. [a-z]{3}[0-9]{3}[a-z]{3})
Hvor mange kombinationer er det? (ret mange)

Mask attack:

- Udnyt hvordan mennesker designer passwords (e.g. søren1985)

### Good Password

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%202.png)

**Don’t do (NIST 800-63B - 2017)**

- Passwords obtained from previous breach corpuses.
- Dictionary words
- Repetitive or sequen-al characters (e.g. ‘aaaaaa’, ‘1234abcd’).
- Context-specific words (e.g. name of the service, username)
- Password < 8 characters
- Impose other composi-on rules (e.g., mixtures of different character types, consecutively repeated characters)
- Require periodic password change

However, force a change if there is evidence of compromise of the authenticator. Why?

**Do**

- Balance mnemonic (won’t write it down) and complexity (see previous slide)
- Password manager?
- How to choose a good password?

### How to choose a good password

From Bruce Schneier:

1. Choose a personal sentence (easy to memorize for the user)
2. Take initial letters
3. Combine it with some personal tricks (easy to memorize for the user) so that it modifies the sentence to create a robust password.
4. Use it as a master password in a password manager.

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%203.png)

### Server Breach - How to store passwords

Not in cleartext

- What if the password db is violated?
- Adobe’s 2013 data breach leaked 150M records (fucking klassisk Adobe mand…)

Not using encryption

- How to store the key?
    - Solution: Salting + Special HMAC function
    - Salting (random number used once) to minimise dictionary attacks
    - Special function is slower than HMAC to minimise brute-force attacks
    - Salt plays as key in HMAC
    
    ![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%204.png)
    

Dette garanterer ikke confidentiality og er ikke encryption.

En god password DB vil altså i stedet bruge symmetric encryption til at backe dine passwords up.

### Kan hash functions bruges til confidentiality??

Nej. Og derfor er hash functions ikke encryption. 

De kan bruges til integrity!!

Encryption giver confidentiality, men ikke integrity.

## User-Computer Authentication

Often multi-factor (e.g. debit card)

### **Possession-based authentication**

- User identity proved by possessing an object (e.g. smartcard, smart token)
- It may store sensible information
- Different level of security
- Nøglekort vs smart token vs EMV vs Student card vs Rejsekort

Limits

- Authentication process identifies the object rather than the user carrying it
- Losing the object easier than forgetting a secret?

Solution

- Multi-factor authentication
- Multi-factor authentication ≠ Multi-step authentication

### Smart token

Software or (powerful) device

User-smart token authentication often based on knowledge (e.g. PIN)

Generates a one-time password that is accepted once by authenticator

1. Password token (OTP)
Offline - One-time password based on a secret key/seed stored in the smart token 
Based on SK crypto, device and authenticator store the secret key/seed
2. Challenge-response token (U2F)
Online - Password based on a challenge sent by the authenticator
Based on PK crypto, the device stores the secret key
Support other services e.g. signature

User-(remote)computer authentication based on knowledge (e.g. password) + possess (token).

### Smart token -U2F

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%205.png)

### Inherence-based authentication

Unique biometric feature of the user

Physiological (e.g. fingerprint, iris, blood pressure, hand traits, etc.

Behavioural (e.g. signature, voice, keystroke dynamics, etc.)

More expensive than previous approaches

Highest level of security

- Although technically less accurate than previous approaches
- False positive and false negative

It is not a very good idea to send your biometric data to any place your don’t trust to store it safely, since if it’s leaked, it’s leaked, and you can’t change it!

Require sampling of key features

Sampling generates a **template** that best-approximates key features 

Authentication is decided upon comparison of **current** measured feature against **template**

Succes if current and template corresponds given a margin tolerance

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%206.png)

### Inherence-based authentication - Discussion

**Privacy**

- How does the server store the template?
- Can the scanner reproduce features?
- We can replace passwords (which may be even one-time) and objects

**Safety**

- Are iris scanners dangerous for the eye?
- Finger-chopping fear (someone is gonna cut off my finger to access my phone :(((((( )

**Security**

- How hard is it to fool iPhone fingerprint sensor=
- And Samsung iris scanner?

### Fingerprint

**Pattern ridges** on hands and feets, which are determined before birth.

Pattern ridges are unique and don’t change over the years.

Well-known method in forensics, used as signature in ancient Babylon.

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%207.png)

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%208.png)

# Access Control

You don’t want users to be able to access each others data. 

Access control is enabling actions and data for specific users based on their identity.

## RFC 4949 - Security glossary

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%209.png)

## Access control Intro

**Authorization** - Granting of *right* or *permission* to a *system entity* to access a *resource*.

**Audit** - review or examination of system records (logs)

Access control mediates between User and System resources. Steps: 

1. Authentication
2. Permission check
3. Maintenance of permission DB
4. Auditing & monitoring

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%2010.png)

### Subjects, objects, and access rights

**Subject** - entity capable of accessing objects; typically a process

Basic access control (e.g. Unix): **owner, group, world**

**Object** - resources with restricted access (e.g. files, db records, time on a cluster)

Access rights: **read, write, execute, delete, create, search**

## Discretionary Access Control (DAC)

Controls access based on the identity of the requestor and on access rules stating what requestors are (or are not) allowed to do.

Discretionary: entities allow/disallow other entities to access resources (entity = user)

- Typically implemented by databases, operating systems
- Access control matrix: subjects X resources → access right
    - Subjects: users or groups
    - Resources: records, file, Dbs
- Column view: Access control lists
- Row view: capability tickets

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%2011.png)

### ACLs in Unix (Linux, macOS/iOS, BSD)

Minimal ACLs:

read, write, execute for owner, group, other (9bit)

Extended ACLs:

read, write, execute for owner & others,

rwe bits for group act as a mask for the ACLs

Use setfacl tool to define access control lists

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%2012.png)

### Some extra bits

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%2013.png)

## Role-based access control

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%2014.png)

### Role hierarchies

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%2015.png)

## Attribute-based Access Control (ABAC)

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%2016.png)

### ABAC scenario

![image.png](Lecture%208%20-%20Authentication%20and%20Access%20Control%2012857d12e9668015ae70ff5bebd8edca/image%2017.png)

## Mandatory access control in practice: SELinux (Android, RedHat)

It evaluates actions attempted by subjects against objects.

**Subjects**=processes, **permissions**=actions, **objects** are of different classes

Example object classes: *file, dir, socket, tcp_socket, unix_stream_socket, file system, node, xserver, cursor*

Example permissions: *search, rmdir, getattr, remove_name, reparent*

### SELinux principles

2 principles to rule them all:

- All that is not permitted is denied
- Subjects, permissions and objects are grouped