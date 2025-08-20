# Chapter 2: Application Layer

## 2.1 Principle of Network Applications

- **Client-Server Architecture**: In a client server architecture, there is a dedicated server that services requests from multiple client hosts. Clients do not directly communicate with each other but interact with the server. The server has a fixed, well-known IP address. Examples include the Web, FTP, Telnet, and email.
- **Peer-to-Peer (P2P) Architecture**: In a P2P architecture, there is minimal reliance on dedicated servers in data centers. Peers, which are intermittently connected hosts, communicate directly with each other without a dedicated server intermediary.
- **P2P Scalability**: P2P architectures offer self scalability, with peers contributing service capacity by distributing files to other peers. They are cost effective and do not require significant server infrastructure.
- **Challenges of P2P Architectures**: P2P applications face challenges related to security, performance, and reliability due to their highly decentralized structure.
- **Communication Between Processes**: Processes running on different end systems communicate with each other by exchanging messages across the computer network.
- **Socket**
-
- Socket communication is a mechanism that enables two processes, possibly on different machines, to communicate over a network. A socket is defined by an IP address and a port number. TCP sockets provide reliable, connection-oriented communication, while UDP sockets provide faster, connectionless communication..

<img src="https://lh3.googleusercontent.com/pw/ADCreHfjdzN47NUqgVF6Leej5qKJLDdzI8ZtOIy4Gbq0EoANrQ8oLeWTBbPJ8_oCehHJG19bSWgldXa86Lw0hEMNjGrGleqJBJijilrs61lEfjnfH26Fy_3VD2Qe_voulh7kOk_Q0Fk0nfvo490o_3tOK-zZ=w1920-h940-s-no" width="680" height="350">

- **Addressing Processes**: To send messages between processes, the receiving process's address needs to be specified. This includes the host's IP address and a destination port number. The IP address identifies the host, while the port number identifies the specific receiving process.
- **Port Numbers**: Popular applications are assigned specific port numbers (e.g., Web server on port 80, mail server on port 25)



## 2.3 Application Layer Protocol: Web and HTTP
- HTTP (HyperText Transfer Protocol) is an application-layer protocol used for communication on the World Wide Web. It defines how a client (browser) and a server exchange messages in the form of requests and responses. HTTP runs on TCP port 80 and is stateless (each request is independent).

- **HTTP**: `HTTP (HyperText Transfer Protocol)` is the primary application layer protocol of the World Wide Web. It relies on client and server programs that communicate by exchanging HTTP messages. Web pages are composed of objects, which are individual files with unique URLs.
- **Web Page Structure**: A web page typically includes a base HTML file and referenced objects like images, stylesheets, and videos. Objects are identified by URLs, which consist of a `hostname` and a `path name`.
- **HTTP and TCP**: HTTP uses TCP (Transmission Control Protocol) as its underlying transport protocol. Clients initiate TCP connections with servers to exchange HTTP messages.

> The HTTP client first initiates a TCP connection with the server. Once the connection is established, the browser and the server processes access TCP through their socket interfaces. 

> HTTP need not worry about lost data or the details of how TCP recovers from loss or reordering of data within the network. 

- **Stateless Protocol**: HTTP is a stateless protocol, meaning servers `don't store client specific information.` If a client requests the same object multiple times, the server doesn't remember previous requests.
- **HTTP Versions**: `HTTP/1.0` and `HTTP/1.1` are common versions, with HTTP/1.1 supporting persistent connections. Newer versions like HTTP/2 are also emerging.
### 2.3.1 Non Persistent and Persistent Connections 
- Non persistent connections create a new connection for each requested object. Persistent connections allow multiple objects to be sent over the same connection, improving efficiency.

> Although HTTP uses persistent connections in its default mode, HTTP clients and servers can be configured to use non persistent connections instead.

> round trip time (RTT), which is the time it takes for a small packet to travel from client to server and then back to the client. The RTT includes packet propagation delays, packet queuing delays in intermediate routers and switches, and packet processing delays.

<img src="https://lh3.googleusercontent.com/pw/ADCreHcP6O3E33NG7QnDmzX1ZUYsYN4WdmaGZSwLxO79aCwgpc2VRQI5lV8oSDjGyga6BN6nbLTnXzZnfZe49s3o9JvbZT35Z1vqiUG1c97LMJbYwZwMhTgBitpNwl5znilEEFnGID7QpG4z98mGuwdk6xPg=w1456-h1130-s-no" width="520" height="520">

- The three way handshake involves the client and server exchanging messages, taking one round trip time (RTT) for this process.
- After completing the handshake, the client sends an HTTP request message along with an acknowledgment into the TCP connection.
- The server responds by sending the HTML file over the established connection.
- The total response time is approximately two RTTs plus the transmission time for the HTML file.

| Feature                   | Non-Persistent HTTP        | Persistent HTTP    |
| ------------------------- | -------------------------- | ------------------ |
| TCP connection per object | Yes                        | No (reused)        |
| Overhead                  | High (multiple handshakes) | Low                |
| Speed                     | Slower                     | Faster             |
| Standard Version          | HTTP/1.0                   | HTTP/1.1 and later |

### Non-Persistent HTTP (HTTP/1.0)

* Each object requires:

  1. **TCP connection setup** (3-way handshake = 1 RTT).
  2. **HTTP request + response** (1 RTT).
* So, **2 RTTs per object** (ignoring data transmission time).
* If a page has `N` objects → `2N RTTs`.

### Persistent HTTP (HTTP/1.1+)

* First object:

  * 1 RTT for TCP setup + 1 RTT for request/response = **2 RTTs**.
* Remaining `N-1` objects:

  * Only 1 RTT each (request/response).
* Total = `2 + (N-1)` RTTs = `N + 1 RTTs`.



### 2.3.2 HTTP Message Format: 

- HTTP messages have two types: `request messages` and `response messages`. Request messages include a method (e.g., GET), URL, and HTTP version, followed by header lines. Response messages include a `protocol version`, `status code` (e.g., 200 OK), and `header lines`, followed by the `entity body`. [Click here for more info](https://github.com/VasanthVanan/web-application-hackers-handbook-notes/blob/main/Chapters/Chapter-3%20Web%20Application%20Technologies.md#311-http-requests)

```http
GET /somedir/page.html HTTP/1.1 \r\n
Host: www.someschool.edu \r\n
Connection: close \r\n
User-agent: Mozilla/5.0 Accept-language: fr \r\n
```

```http
HTTP/1.1 200 OK \r\n
Connection: close \r\n
Date: Tue, 18 Aug 2015 15:44:04 GMT \r\n
Server: Apache/2.2.3 (CentOS) \r\n
Last-Modified: Tue, 18 Aug 2015 15:11:03 GMT \r\n
Content-Length: 6821 \r\n
Content-Type: text/html \r\n
\r\n

(data data data data data ...)
```

- **Header Lines**: Header lines provide additional information in HTTP messages. Examples of request headers include `Host`, `Connection`, `User-agent`, and `Accept-language`. Examples of response headers include `Connection`, `Date`, `Server`, `Last-Modified`, `Content-Length`, and `Content-Type`.
- **Status Codes**: Status codes (e.g., 404 Not Found) indicate the result of an HTTP request. [Click here for more info](https://github.com/VasanthVanan/web-application-hackers-handbook-notes/blob/main/Chapters/Chapter-3%20Web%20Application%20Technologies.md#318-status-codes)
- **HTTP Methods**: HTTP includes methods like GET, POST, PUT, and DELETE for different types of requests and actions.
- **Entity Body**: The entity body in HTTP messages contains data related to the request method.


### 2.3.5 HTTP/2 and HTTP/3

### **HTTP/2 (2015)**

* **Transport**: Runs over **TCP**.
* **Multiplexing**: Multiple requests/responses in one TCP connection (no head-of-line blocking at HTTP level).
* **Header Compression**: Uses HPACK to reduce redundant header data.
* **Binary Protocol**: More efficient than text-based HTTP/1.1.
* **Server Push**: Server can send resources before the client requests them.
* **Limitation**: Still suffers from **TCP-level head-of-line (HOL) blocking**. If one packet is lost, all streams in that TCP connection wait.

---

### **HTTP/3 (2022, based on QUIC)**

* **Transport**: Runs over **QUIC**, which is built on **UDP** (not TCP).
* **Multiplexing**: Independent streams → no TCP HOL blocking. Packet loss only affects the affected stream, not others.
* **Built-in Encryption**: QUIC integrates TLS 1.3 (security by default).
* **Faster Connection Setup**: 0-RTT and 1-RTT handshakes, reducing latency.
* **Better Performance on Unstable Networks**: Designed for mobile/wireless where packet loss is common.
* **Adoption**: Used by Google, Facebook, Cloudflare, YouTube, etc.

> QUIC Protocol (Quick UDP Internet Connections) is a transport layer network protocol designed to improve the performance and security of internet connections, particularly for web applications.

### Key Differences

| Feature             | HTTP/2                                | HTTP/3                       |
| ------------------- | ------------------------------------- | ---------------------------- |
| Transport Protocol  | TCP                                   | QUIC (UDP-based)             |
| Multiplexing        | Yes, but affected by TCP HOL blocking | Yes, no HOL blocking         |
| Security            | TLS optional                          | TLS 1.3 built-in (mandatory) |
| Connection Setup    | TCP handshake + TLS (2–3 RTT)         | QUIC 0-RTT/1-RTT (faster)    |
| Network Suitability | Stable wired connections              | Mobile, high-loss networks   |



### **HTTP/1.0 (non-persistent)**

* Each object needs:

  * 1 RTT for TCP handshake + 1 RTT for request/response = **2 RTTs per object**.
* For `N` objects → `2N RTTs`.
* Browsers sometimes opened 4–6 parallel TCP connections to reduce delay, but still inefficient.

---

### **HTTP/1.1 (persistent)**

* First request: **2 RTTs** (TCP handshake + request/response).
* Each additional object: **1 RTT** (since connection reused).
* Total: **N + 1 RTTs**.
* Example: 5 objects → `6 RTTs` vs `10 RTTs` in HTTP/1.0.

---

### **HTTP/2 (multiplexing)**

* One TCP handshake (1 RTT) + TLS handshake (1 RTT, optional) + request/response.
* All objects sent in parallel over **one TCP connection**.
* Total: About **2 RTTs + transmission time**, regardless of number of objects.
* Problem: **TCP Head-of-Line blocking** → if one packet is lost, all streams stall.

---

### **HTTP/3 (QUIC over UDP)**

* QUIC handshake integrates transport + TLS in **1 RTT**, sometimes **0 RTT** (if session resumption).
* Multiplexed streams over UDP → no head-of-line blocking.
* Total: **\~1 RTT + transmission time**.
* Best for lossy/wireless networks where retransmissions are common.

---

### Quick Comparison Table

| Version  | Connections    | RTTs Needed (N objects)     | Limitation                            |
| -------- | -------------- | --------------------------- | ------------------------------------- |
| HTTP/1.0 | New per object | **2N RTTs**                 | Very slow                             |
| HTTP/1.1 | Persistent     | **N+1 RTTs**                | Still sequential, no true parallelism |
| HTTP/2   | Multiplexed    | **\~2 RTTs total**          | TCP HOL blocking                      |
| HTTP/3   | QUIC (UDP)     | **1 RTT (0 in some cases)** | Newer adoption, not everywhere        |


### 2.3.3 Cookies

- There are situations where web sites need to identify users, for security or personalization purposes. HTTP uses cookies to achieve user identification and tracking.
- Cookies have four components: a `cookie header` in HTTP `response` and `request` messages, a `cookie file` on the user's end system, and a `back end database` on the web site.

<img src="https://lh3.googleusercontent.com/pw/ADCreHfFwZxxD_q6lNIW4MotRBCCUUmdnTTAst3aa9ByyF1GoQxQGr9oMpd-3hudmL_VvIqWZhb9sF4Dsw3YYeV3N38qe-HBB9afByGpuvPj1gSfGeATqwiuckHdhRVluCOM_E_NXmqLYBN82wpku2x_BUd1=w1326-h1130-s-no" width="620" height="630">

- Cookies work by sending a unique identification number in a `Set-cookie` header from the server to the user's browser.
- The browser stores the identification number and sends it back to the server in a Cookie header with subsequent requests.
- Cookies are used to track user activity and offer personalized services, like shopping carts or recommendations.
- Users can be identified over multiple sessions by maintaining the same identification number in cookies.
- Cookies are controversial due to potential privacy concerns, as websites can gather and potentially sell user information.

### 2.3.4 Web Caching

- Web caches, or proxy servers, handle HTTP requests on behalf of origin servers.
- Caches store copies of requested objects, reducing the need to fetch them from the origin server.
- Users can configure browsers to direct requests through caches for faster responses.
- Caches serve as both servers (to clients) and clients (to servers) in the caching process.
- Installed by ISPs and institutions, caches enhance performance and lower bandwidth costs.
- Benefits include faster responses, reduced bandwidth upgrades, and decreased overall Internet traffic.
- Content Distribution Networks (CDNs) use distributed caching to localize content delivery.

> An HTTP request message is a so called conditional GET message if (1) the request message uses the GET method and (2) the request message includes an If-Modified-Since: header line.

- `Conditional GET` checks for freshness by comparing the `If-Modified-Since` header with object modification date.
- If an object hasn't changed, a `304 Not Modified response` allows the cache to serve the locally cached object.

> value of the If-modified-since: header line is exactly equal to the value of the Last-Modified: header line that was sent by the server initially.

### Caching vs Cookies in Networking

#### **Caching**

* **Purpose**: Reduce load time and bandwidth by storing copies of resources (HTML, images, scripts) locally.
* **Where stored**: Browser cache, proxy server, or CDN edge servers.
* **Content**: Static or dynamic web resources.
* **Control**: HTTP headers like `Cache-Control`, `Expires`, `ETag`.
* **Example**: A logo image downloaded once, then reused from local cache on future visits.

#### **Cookies**

* **Purpose**: Store small pieces of **stateful information** about the user.
* **Where stored**: User’s browser (text file).
* **Content**: User session data, authentication tokens, preferences, tracking IDs.
* **Control**: Server sets cookies using `Set-Cookie` header, browser sends them back in subsequent requests.
* **Example**: Staying logged in on a website, remembering items in a shopping cart.



### Key Differences

| Feature      | Caching                                     | Cookies                                       |
| ------------ | ------------------------------------------- | --------------------------------------------- |
| Function     | Speeds up loading by reusing stored content | Stores user/session data                      |
| Data stored  | Web resources (HTML, CSS, images, JS)       | Key-value user data (session ID, preferences) |
| Storage size | Large (MBs of files)                        | Small (usually ≤ 4 KB per cookie)             |
| Location     | Browser cache, proxy, CDN                   | Browser storage sent with requests            |
| Impact       | Performance optimization                    | Personalization, authentication, tracking     |



## 2.4 Application Layer Protocol: SMTP


### **Definition**

* **SMTP** = Simple Mail Transfer Protocol.
* An **application layer protocol** used for sending and relaying electronic mail over the Internet.
* Works on **TCP port 25** (default), also 465 (SMTP over SSL), and 587 (SMTP with STARTTLS).

---

### **Purpose**

* Defines how email is **sent** from:

  * **Client → Mail server**
  * **Mail server → Mail server** (relay)
* Note: For **retrieving** emails, protocols like **POP3** or **IMAP** are used, not SMTP.

---

### **How SMTP Works (Process Flow)**

1. **Composition**: User writes an email in client software (MUA = Mail User Agent, e.g., Outlook, Gmail).
2. **Submission**: Client sends the email to **SMTP server (MSA – Mail Submission Agent)** using SMTP.
3. **Transfer**: SMTP server forwards email to recipient’s **Mail Transfer Agent (MTA)**. If recipient is on another domain, SMTP relays it over the Internet.
4. **Delivery**: Final server stores the mail in recipient’s **Mailbox (MDA – Mail Delivery Agent)**.
5. **Retrieval**: Recipient fetches email using **POP3 or IMAP**, not SMTP.

---

### **SMTP Commands and Replies**

SMTP uses text-based commands between client and server.

* **HELO / EHLO** → Identify the client to server.
* **MAIL FROM:** → Sender’s address.
* **RCPT TO:** → Recipient’s address.
* **DATA** → Begin transfer of message body.
* **QUIT** → End session.

**Reply Codes (3-digit):**

* 220 → Service ready.
* 250 → Requested action completed.
* 354 → Start mail input.
* 421 → Service unavailable.
* 550 → Requested action not taken (e.g., user unknown).

---

### **Characteristics**

* **Push protocol**: Sender pushes mail to server.
* **Text-based**: Commands and responses are human-readable.
* **Relies on TCP**: Ensures reliable transmission.
* **Store-and-forward**: Servers can queue emails if the recipient server is unavailable.

---

### **Limitations**

* SMTP can only **send** mail, not retrieve.
* By default, no encryption (can be intercepted). → Fixed by using **SMTPS (SSL/TLS)**.
* Basic spam and spoofing protections (SPF, DKIM, DMARC) added later.


### 2.4.3 Mail Message Structure

- Email messages consist of a `header` and a `body`.
- The header includes sender and recipient information, such as `"From," "To," and "Subject."`. The header lines and the body of the message are separated by a blank line (that is, by CRLF).
- These headers are distinct from SMTP commands used for server handshake communication.

```http
From: alice@crepes.fr
To: bob@hamburger.edu
Subject: Searching for the meaning of life.
```

### 2.4.4 Mail Access Protocols

<img src="https://lh3.googleusercontent.com/pw/ADCreHe0fyv4ULp_uamEsceCVVhVIa89gH-EYeg8F5QQ9MJOB6_HPfvS8QpwFXnBbpd_o5WBJf3SYSGt_KwkgMRBQ0BUtFHZP6lTTLAvPlWIfoypiutfj2fm5ZktaSNOuMKNcfdEXXH7OafVuFbqC-vIcfa4=w1876-h442-s-no" width="680" height="220">

> Bob’s user agent can’t use SMTP to obtain the messages because obtaining the messages is a pull operation, whereas SMTP is a push protocol.

- Users retrieve their email messages from a shared mail server using either HTTP or IMAP.
- HTTP is often used for web based email clients like Gmail, while IMAP is common with clients like Microsoft Outlook.
- Both the HTTP & IMAP approaches allow to manage folders, move messages to folders, delete messages, mark messages as important, and so on.

### Email Protocols: SMTP vs POP3 vs IMAP

---

### **SMTP (Simple Mail Transfer Protocol)**

* **Purpose**: **Sending/relaying emails** from client to server, or server to server.
* **Ports**: 25 (default), 465 (SSL), 587 (TLS).
* **Flow**: Outgoing mail only.
* **Nature**: Push protocol.

---

### **POP3 (Post Office Protocol v3)**

* **Purpose**: **Retrieving emails** from mail server to client.
* **Ports**: 110 (default), 995 (SSL).
* **Working**:

  * Downloads emails from server to local machine.
  * By default, deletes from server after download (can be configured to leave copies).
* **Characteristics**:

  * Simple and lightweight.
  * No synchronization across multiple devices.
  * Good if user checks mail from one device only.

---

### **IMAP (Internet Message Access Protocol)**

* **Purpose**: **Retrieving and managing emails** from mail server.
* **Ports**: 143 (default), 993 (SSL).
* **Working**:

  * Keeps emails on the server.
  * Allows viewing, organizing, and searching without full download.
  * Syncs across multiple devices.
* **Characteristics**:

  * Server-side storage.
  * Supports folders, read/unread status, multiple clients.
  * Heavier on resources than POP3.

---

### **Key Differences**

| Feature          | SMTP (Send)      | POP3 (Receive)                         | IMAP (Receive)         |
| ---------------- | ---------------- | -------------------------------------- | ---------------------- |
| Main Use         | Sending/relaying | Downloading                            | Synchronizing          |
| Ports            | 25/465/587       | 110/995                                | 143/993                |
| Direction        | Outgoing only    | Incoming only                          | Incoming only          |
| Storage          | N/A              | Local (deletes from server by default) | Server (keeps copy)    |
| Multi-device use | Not applicable   | Poor                                   | Excellent              |
| Sync features    | N/A              | None                                   | Full (folders, status) |

## 2.5 Application Layer Protocol: DNS

**DNS (Domain Name System)**

* A distributed naming system that translates **human-readable domain names** (e.g., `www.google.com`) into **machine-readable IP addresses** (e.g., `142.250.182.206`).
* Works like the "phonebook of the internet."
* Essential because humans remember names, but network communication requires IP addresses.

---

### **Formal Definition (Interview-ready)**

> "DNS is a hierarchical, distributed database system that resolves domain names into IP addresses, enabling users to access resources on the internet without needing to remember numerical addresses."

---

- DNS is an essential service that translates human friendly hostnames into IP addresses.
- It's a distributed database and an application layer protocol, implemented with `DNS servers`, often running `BIND` software and runs over UDP and uses port 53.

> People prefer the more mnemonic hostname identifier, while routers prefer fixed length, hierarchically structured IP addresses.

- DNS services include:
    - **hostname aliasing**: host with a complicated canonical hostname can have one or more alias names.
        ```http
        relay1.west-coast.enterprise.com (canonical/official website name)
        enterprise.com (alias name)
        ```
    - **Mail Server Aliasing**: DNS resolves alias hostnames to canonical forms for mail servers and retrieves corresponding IP addresses.
        ```http
        bob@yahoo.com --> bob@relay1.west-coast.yahoo.com
        ```
    - **Load Distribution**: DNS balances traffic among replicated servers by rotating IP addresses within replies, ensuring even distribution. This technique is also applied to email servers with shared alias names.

### 2.5.1 How DNS Works: High Level Overview

> gethostbyname() is the function call that an application calls in order to perform the translation.

- DNS operates through query and reply messages using UDP datagrams on port 53.
- DNS queries involve multiple servers globally distributed.
- A simple centralized design for DNS is not feasible due to scalability issues.
- Issues with centralized design: `single point of failure,` `high traffic volume`, `distant database`, and `maintenance`.
- DNS uses a hierarchical structure and a distributed database., to handle the vast number of hosts on the Internet.

### 2.5.2 Distributed, Hierarchical Database


<img src="https://lh3.googleusercontent.com/pw/ADCreHfjtoFE2ozufMyfFi_xvvvjhwhvWHxaFcgn2jVCEG50nQsaQlTqhQQovC1HaJrlB0h8La--jGtCdoz8c6RxZVLsou9ISfsTEy7uaS-fjCMZNBiZtfTPnFpbVbYUDbQ49wyFPKQJJNUc-_7h4wmYm2IX=w1920-h710-s-no" width="580" height="220">

- DNS uses three classes of servers: `Root` DNS servers, `top level domain (TLD)` DNS servers, and `authoritative` DNS servers.
- Root DNS servers provide IP addresses for TLD servers. TLD servers provide IP addresses for authoritative DNS servers Authoritative DNS servers store DNS records for specific organizations.
- A `local DNS server`, specific to an ISP, also plays a crucial role in DNS queries. It cache DNS information to reduce query traffic and improve performance.

> When a host makes a DNS query, the query is sent to the local DNS server, which acts a proxy, forwarding the query into the DNS server hierarchy.

- DNS extensively utilizes caching to enhance performance. These are stored temporarily and it allows DNS servers to quickly respond to subsequent queries for the same hostname.

### 2.5.3 Recursive vs Iterative DNS Queries

<img src="https://lh3.googleusercontent.com/pw/ADCreHcDzbK4FY8RExEyQO82XsXu_OFQXOqMXfJx6q8TO_Tx4wYRJt9WaiktQr-4bF482giEXJmGfkLMszdS7Ufn_sjYphuuVOdpKVn7RI6laoHLFKiPUtFpU_kOUnZ_UJN7NjeJdt5Bp65KPlNKkiEpFrIF=w1708-h1044-s-no" width="780" height="520">

### 2.5.4 DNS Records & Messages

- DNS servers store resource records (RRs) in the distributed database.
- A resource record (RR) is a four tuple: `(Name, Value, Type, TTL)`.
- **TTL** (Time to Live) determines when a resource should be removed from a cache.
- Types of resource records:
    - `Type=A`: Maps hostname to IP address.
    - `Type=NS`: Maps a domain to the hostname of an authoritative DNS server.
    - `Type=CNAME`: Provides the canonical name for an alias hostname.
    - `Type=MX`: Maps to the canonical name of a mail server with an alias hostname.

> To obtain the canonical name for the mail server, a DNS client would query for an MX record; to obtain the canonical name for the other server, the DNS client would query for the CNAME record.

- DNS messages have a header section with several fields, including `query/reply` flags, `recursion` flags, and more.
- DNS messages consist of a question section, answer section (resource records), authority section, and additional section.

> A 1 bit query/reply flag indicates whether the message is a query (0) or a reply (1). A 1 bit authoritative flag is set in a reply message when a DNS server is an authoritative server for a queried name. 

> A 1 bit recursion desired flag is set when a client (host or DNS server) desires that the DNS server perform recursion when it doesn’t have the record. 

> A 1 bit recursion available field is set in a reply if the DNS server supports recursion. 

### 2.5.5 Inserting Records to DNS Database

> A registrar is a commercial entity that verifies the uniqueness of the domain name, enters the domain name into the DNS database (as discussed below), and collects a small fee from you for its services.

- To register a domain name, you need to provide registrar with DNS server names and IP addresses. Registrar enters `Type NS` and `Type A` resource records for `authoritative` DNS servers into `TLD` servers.
- Additional resource records, like Type A and Type MX, must be added for Web and mail servers.

