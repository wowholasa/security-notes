# Lecture 9 - 30.10.2024 - Penetration Testing

# Vulnerability Type Change by Year

## Nist

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image.png)

Rise of no information: Not good, because we don’t know what is going on 

## Mitre

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%201.png)

Devs write vulnerable code. There is no way to avoid this. Perfect code does not exist

# Pentesting

1. Target Acqusition
2. Information gathering
3. Initial Access
4. Violate integrity/Confidentiality
5. Privilege Escalation
6. Maintain Access
7. ~~Covering Tracks~~ Reporting

# Warmup

## Web

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%202.png)

## URL

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%203.png)

## HTTP

- Hypertext Transport Protocol
- Stateless
- Text-based request-reply protocol

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%204.png)

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%205.png)

## Web Server

- Takes HTTP requests on TCP port 80 (HTTPS on port 443)
- Reply to HTTP request by looking at internal “routing” table
    - E.g. *workbench/saved/1230.html → /var/www/workbench/saved/1230.html*
- Many web servers launch external program/interpreters to generate the return page
    - E.g. *PHP, Python, Perl, [ASP.NET](http://ASP.NET), Java, …*

### Web Server + Database

- Recall: HTTP is stateless
- So, web applications use (No)SQL databases as permanent storage
- Web application languages (PHP, Java, ASP.NET, etc.) make queries by piecing together SQL commands as strings
- Vulnerable to injections

## Terminology

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%206.png)

Payload:

Exploit:

Vulnerability:

## Target Acquisition & Information gathering

- Black-box audit
- Goal: finding potential vulnerabilities

- Use nmap, nc, HTML inspector, JS debugger, etc.

 

### Black-box audit

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%207.png)

# Injection attacks

- Attacker exploits data being treated as code
- Target: web server

- Common variants
    - Command injection
    - Code injection
        - SQL injection

## Command Injection

- Virtuemart allow a visitor of the shop to create a PDF file of her order
- Interesting bites of “shop.pdf_output.php”

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%208.png)

The link they expect:

- https://bob/index.php?page=shop.pdf_output&option=com_virtuemart&showpage=index.php

The link we try to give them:

- https://bob/index.php?page=shop.pdf_output&option=com_virtuemart&showpage=’;ls;’
    - So we try to run ls at the end

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%209.png)

**Countermeasure:**

- Sanitize input
    - e.g. replace/ban arguments with ‘;’
        
        Use PHP sanitization/filter
        

## SQL Injection

- Extremely popular variant of code injection
- Attacker supplies SQL commands as input
- Web-server passes these commands to database engine

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%2010.png)

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%2011.png)

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%2012.png)

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%2013.png)

**Countermeasure:**

- Sanitize input

e.g.

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%2014.png)

## Cross-site scripting attacks (XSS)

- Attacker exploits data being treated as code
- **Target: Client**

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%2015.png)

Types:

- Server XSS
    - Vulnerability is in the server (the payload is in the response page)
- Client XSS
    - Vulnerability is in the client side (payload **NOT** in the response page)

### Server XSS

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%2016.png)

### Server XSS - Cookie Hijacking

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%2017.png)

### Client XSS

![image.png](Lecture%209%20-%2030%2010%202024%20-%20Penetration%20Testing%2012f57d12e96680b19262d827ea35baa7/image%2018.png)