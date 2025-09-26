## What Happens When You Type `https://www.google.com` and Press Enter?

When preparing for software engineering interviews, one of the most classic and challenging questions is: **“What happens when you type a URL into your browser and press Enter?”**  
This question looks simple, but the answer reveals a lot about your understanding of networking, security, and how the web actually works behind the scenes.  

In this article, I will walk you through the journey step by step, covering the required topics: **DNS request, TCP/IP, Firewall, HTTPS/SSL, Load-balancer, Web server, Application server, and Database.**

---

## 1. DNS Request – Finding the Address
When you type `www.google.com`, your browser first needs to know *where* that server lives on the Internet. Humans use names, but machines need IP addresses.

- The browser checks local caches (browser cache, operating system cache).
- If not found, it asks a **DNS resolver** (often provided by your ISP or a public service like Google DNS).
- The resolver queries authoritative DNS servers until it finds the correct IP address for `www.google.com`.
- Finally, the IP address is returned to your computer, and now the browser knows *where to connect*.

---

## 2. TCP/IP – Establishing a Connection
Now that the browser knows the destination IP, it must open a communication channel.

- A **TCP connection** is created with a three-way handshake (SYN, SYN-ACK, ACK).
- The communication travels over the **IP protocol**, which ensures routing from your computer to Google’s server across many networks.
- This guarantees that packets arrive reliably and in order.

---

## 3. Firewall – Security Gateways
Along the way, the traffic passes through multiple **firewalls**:

- Your personal computer firewall,
- Your network’s firewall (home router, company network),
- ISP-level and Google’s perimeter firewalls.

Each firewall checks if the connection is legitimate, blocks unwanted traffic, and ensures the communication follows security policies.

---

## 4. HTTPS/SSL – Securing the Communication
Because the URL starts with `https://`, the connection must be encrypted.

- The browser and server perform a **TLS handshake**.
- The server presents its **SSL/TLS certificate**, proving it is indeed Google.
- Keys are exchanged securely, and encryption is established.
- From this point forward, all traffic is **encrypted and safe** from eavesdropping.

---

## 5. Load Balancer – Distributing the Work
Google doesn’t rely on just one server. Instead, the request goes through a **load balancer**.

- The load balancer chooses which server should handle your request based on location, traffic, and availability.
- This ensures speed, fault tolerance, and scalability.

---

## 6. Web Server – Handling the Request
The chosen server receives your request. A **web server** such as Nginx or Apache:

- Understands the HTTP request,
- Applies rules (compression, caching, headers),
- For static files (like images or CSS), it may respond immediately.

If more complex processing is needed, it forwards the request to the application server.

---

## 7. Application Server – Running the Logic
The **application server** is where the business logic lives.

- It processes your request (e.g., searching for results).
- It may contact other services and APIs.
- It prepares a response, often by querying a database.

---

## 8. Database – Storing and Retrieving Data
Behind the application lies a **database**.

- The database stores structured information (users, search indexes, logs, etc.).
- The application queries the database and retrieves the relevant data.
- Results are sent back through the application server, then the web server.

---

## 9. Response Back to the Browser
The server response travels back through the load balancer, across the Internet, through firewalls, and finally arrives at your browser.  

The browser then:
- Parses the HTML,
- Loads CSS and JavaScript,
- Renders the page, and
- Displays Google’s search homepage on your screen.

---

## Visual Summary

Here is a simple diagram summarizing the journey:

## Request Flow Diagram


```mermaid
graph TD
  A[Client (browser)]
  B[Local DNS Server]
  C[Firewall / NAT]
  D[Load Balancer]
  E[Web Server (HTTPS port 443)]
  F[TLS termination]
  G[Application Server]
  H[Database]

  A -- DNS query --> B
  B -- IP address --> A

  A -- HTTPS request (TLS) --> C
  C -- Allow/inspect --> D
  D -- Distribute request --> E
  E --> F

  F -- Process request --> G
  G -- Queries database --> H
  H -- Results --> G

  G -- HTML/JSON --> F
  F -- Encrypted response (TLS) --> A
```

---

## Conclusion
So, what happens when you type `https://www.google.com` and press Enter?  
You trigger a fascinating chain of events: from **resolving a domain name, building a secure connection, and passing through firewalls and load balancers**, to reaching **servers and databases that deliver content back to you in milliseconds**.

Understanding this flow demonstrates strong knowledge of networking and web technologies—a skill that is valuable in many software engineering roles.  

Next time you open your browser, you’ll know the incredible journey hidden behind a single keystroke.
 
 Read article on [Medium]()
