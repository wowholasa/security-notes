# Lecture 1 - Introduction and Security Principles

# Security Model

## What is Cybersecurity?

Protecting the data that the systems processes.

Protecting from the adversary. This could be:

- Vandals
- Activists
- Criminals
- States

![image.png](Lecture%201%20-%20Introduction%20and%20Security%20Principles%20685fd10306f94984be46b2eb242fc306/image.png)

## FE (CFCS) threat assessment

- CFCS vurderer, at truslen fra cyberspionage forsat er MEGET HØJ. Det er meget sandsynligt, at danske myndigheder og virksomheder vil blive ramt af forsøg på cyberspionage inden for de næste to år. Det er særligt Rusland og Kina, der benyBer cyberangreb til at få viden…
- På samme måde er truslen fra cyberkriminalitet MEGET HØJ. Cyberkriminalitet rammer bredt, og vi vurderer, at de økonomisk motiverede cyberkriminelle oFe er velorganiserede og robuste overfor myndighedernes indgriben.
- Truslen fra cyberaktivisme er nu HØJ – og altså på det højeste niveau, siden CFCS i 2016 udgav den første årlige trusselsvurdering. Truslen kan kædes direkte sammen med krigen i Ukraine og de mange pro-russiske hackere, der tyer til tastaturet for at vise deres støtte til Rusland…
- Truslen fra destruktive cyberangreb er LAV. Vi vurderer fortsat, at det er mindre sandsynligt, at danske myndigheder og virksomheder vil blive mål for et destruktivt cyberangreb…
- Endelig er truslen fra cyberterror fortsat INGEN. Cyberterror er alvorlige cyberangreb, der skal opnå samme effekt som konventionelle terrorangreb. Truslen har været INGEN flere år i træk, men CFCS følger den tæt, fordi Center for Terroranalyse ved PET vurderer, at truslen fra konventioonel terror mod Danmark er i niveauet alvorlig.

## Security Assumptions

Each (technical/non-technical) assumption is a potential vulnerability.

![image.png](Lecture%201%20-%20Introduction%20and%20Security%20Principles%20685fd10306f94984be46b2eb242fc306/image%201.png)

### Passwords

![image.png](Lecture%201%20-%20Introduction%20and%20Security%20Principles%20685fd10306f94984be46b2eb242fc306/image%202.png)

![image.png](Lecture%201%20-%20Introduction%20and%20Security%20Principles%20685fd10306f94984be46b2eb242fc306/image%203.png)

## Security Goals

### Confidentiality

We don’t want people to see our data, if they aren’t supposed to. 

Keeping information secret.

- Attacks: eavesdropping, man-in-the-middle

### Integrity

- Attacks: masquerading, message tampering, replaying

### Availability

That systems are up and running when they are supposed to. 

- Attacks: Denial of Service, distributed denial of service

### Security Goals continued

- Hvad vil det sige at et system er sikkert?

![image.png](Lecture%201%20-%20Introduction%20and%20Security%20Principles%20685fd10306f94984be46b2eb242fc306/image%204.png)

Confidentiality, integrity og availability er fundamentet. Uden de 3 kan man ikke have de ovenbyggende levels

### Security is impossibly hard

- Du skal forsvarer mod **ALLE** mulige angreb.
- Adversaries skal kun finde **ET** angreb der virker.
- Der findes ikke perfekt security mod alle slags angreb
    - Der vil altid være trade-offs
- Security måles i de ressourcer, der skal anvendes af vores ‘adversary’

# Security Principles

Tommelfingerregler der giver os en sans for hvad der vi skal gøre:

## Economy of Mechanism

Hold det simpelt.

“simplicity”

Komplekse design laver kompleks fejl analyse

## Open Design

Sikkerheden af et system bør ikke være afhængig af hvor hemmelig dets security-mekanismer er.

Adversary kender programmet. 

Systemer er sværre at bygge.

## Minimum exposure

Minimer angrebsoverfladen der fremvises til adversary.

Reducér eksterne interfaces.

Der behøver ikke sendes requests til services, der ikke er nødvendige.

## Least privilege

Ethvert komponent bør kører med det laveste sæt af privilegier nødvendigt.

“En lektorer på ITU har ikke nøgler til sotrage rooms”

## Fail-safe defaults

Systemet bør starte og returnerer til en sikker state, selv hvis der sker en fejl.

Hvis du mister forbindelsen til authentication serveren, så lad være med at lukke nogle ind, mens den er nede.

## Complete mediation

![image.png](Lecture%201%20-%20Introduction%20and%20Security%20Principles%20685fd10306f94984be46b2eb242fc306/image%205.png)

## No single point of failure

Byg redundante sikkerhedsmekanismer når det er muligt

Altså basically det her med at både have passwords og authentication

## Psychological acceptability

Design brugbare sikkerheds mekanismer.

Hjælp brugerne med at lave det rette valg.

## Wrapping up

Adversary: **state-**sponsored cyber attacks

Assumptions: Så få som muligt

Goals: Så mange som muligt

Principles: Så mange som muligt

# Group Theory (To Be Continued in Asymmetric Crypto)

![image.png](Lecture%201%20-%20Introduction%20and%20Security%20Principles%20685fd10306f94984be46b2eb242fc306/image%206.png)

Det her er grunden til at vi ikke laver kryptografiske eksempler det konkrete tal.

## (Abelian) Groups

En abelian gruppe er et par (G, ◦), hvor G er et set og en binær operation ◦ defineret på G sådan at:

- (Closure) For all $g, h \in G, G◦h$ is in G
- There is an identity $e\in G$ such that e◦g=g for gÎG
- Every $g\in G$ has an inverse $h\in G$ such that h◦g = e
- (Associativity) For all $f,g,h\in G$, f◦(g◦h) = (f◦g)◦h
- (Commutativity) For all$g, h \in G$, g◦h = h◦g

The order of a finite group G is the number of elements in G.

## Group Operation

![image.png](Lecture%201%20-%20Introduction%20and%20Security%20Principles%20685fd10306f94984be46b2eb242fc306/image%207.png)

## Cyclic groups

![image.png](Lecture%201%20-%20Introduction%20and%20Security%20Principles%20685fd10306f94984be46b2eb242fc306/image%208.png)

![image.png](Lecture%201%20-%20Introduction%20and%20Security%20Principles%20685fd10306f94984be46b2eb242fc306/image%209.png)

![image.png](Lecture%201%20-%20Introduction%20and%20Security%20Principles%20685fd10306f94984be46b2eb242fc306/image%2010.png)