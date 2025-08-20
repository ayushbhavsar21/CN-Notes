# Chapter 3: Transport Layer


> transport layer -- extending the network layer’s delivery service between two end systems to a delivery service between two application layer processes running on the end systems.


## 3.1 Transport-Layer Services

- The transport layer resides between the application and network layers, providing communication services to application processes on different hosts.
- Transport layer protocols enable `logical communication` between application processes on different hosts, abstracting the physical infrastructure.
- It converts application messages into transport layer `segments`, encapsulated within network layer packets (datagrams) for transmission.
- Transport protocols work only within end systems and are not involved in routing or network core activities.
- These protocol provides communication between application **processes**, while network layer protocol provides communication between **hosts**.

-  IP makes its “best effort” to deliver segments between communicating hosts, but it makes no guarantees. (IP is said to be an unreliable service)

> The most fundamental responsibility of UDP and TCP is to extend IP’s delivery service between two end systems to a delivery service between two processes running on the end systems. Extending host-to-host delivery to process-to-process delivery is called transport layer multiplexing and demultiplexing.

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png)

### Best way to remember TCP vs UDP
- Imagine two cars, each with a bouncing ball inside, driving down a slope. These cars handle the bouncing ball differently in two scenarios:
#### Scenario 1: Car A – Cautious Approach
- Car A is equipped with a protective shield to prevent the ball from bouncing out. The driver is extremely cautious and stops the car every time the ball moves to ensure it remains in the correct spot.
> **Result**: Car A successfully reaches the bottom of the slope with the ball intact. However, the journey is slower because of frequent stops to check on the ball.

#### Scenario 2: Car B – Reckless Approach
- Car B lacks a protective shield and drives down the same slope at high speed. The driver is reckless and doesn’t stop to check on the ball’s position, allowing it to bounce freely and even risk flying out of the car.
> **Result**: Car B reaches the bottom of the slope faster than Car A. Unfortunately, the ball gets lost along the way.

![-----------------------------------------------------](https://raw.githubusercontent.com/andreasbm/readme/master/assets/lines/rainbow.png)

- Key Differences in UDP vs TCP Protocols:

| Aspect                      | UDP (User Datagram Protocol)        | TCP (Transmission Control Protocol)      |
|-----------------------------|----------------------------------|-----------------------------------------|
| Service Model               | Unreliable and connectionless    | Reliable and connection-oriented         |
| Application Selection       | Chosen by the application developer | Chosen by the application developer    |
| Terminology                | Uses "datagram" for segments     | Uses "segment" for segments             |
| Network Layer Protocol     | Operates on top of IP (Internet Protocol) | Operates on top of IP (Internet Protocol) |
| Services Provided          | Process to process data delivery and error checking | Reliable data transfer, flow control, sequence numbers, acknowledgments, timers, and congestion control |
| Reliability                 | Unreliable - Does not guarantee data integrity or delivery | Reliable - Ensures data delivery, integrity, and order |
| Congestion Control         | Unregulated - No congestion control | Regulated - Prevents excessive traffic and aims for fair sharing of network resources |
| Complexity                  | Simpler and less complex         | Complex due to additional services and mechanisms |

## 3.2 Multiplexing and Demultiplexing

**Multiplexing vs Demultiplexing (in Networking, esp. Transport Layer like TCP/UDP)**

---

### **Multiplexing**

* **Definition**: Combining multiple application data streams into a single transport layer stream at the sender.
* **Goal**: Efficiently use the network by sending many app processes’ data over one channel.
* **Key Identifier**: **Port numbers** at source (to tag which application data belongs to).
* **Example**:

  * Your laptop runs Chrome, Zoom, and Spotify.
  * All send data over the same NIC.
  * Transport layer adds **source port numbers** so the receiver can separate them later.

---

### **Demultiplexing**

* **Definition**: Separating a single incoming stream into the correct application processes at the receiver.
* **Goal**: Deliver the right segment to the right app.
* **Key Identifier**: **Destination port number**.
* **Example**:

  * Server gets packets on IP `142.250.182.206`.
  * Based on **destination ports**:

    * Port 80 → web server (HTTP).
    * Port 443 → secure web server (HTTPS).
    * Port 25 → mail server (SMTP).

---

### **Interview-ready one-liner**

> Multiplexing is combining data from multiple processes into one channel at the sender, while demultiplexing is separating that data back to the correct processes at the receiver using port numbers.

---


## 3.5 UDP (User Datagram Protocol)

- UDP is a minimalistic transport protocol. It provides `multiplexing`/`demultiplexing` and minimal `error checking`. Unlike TCP, it adds very little to IP.

> If the application developer chooses UDP instead of TCP, then the application is almost directly talking with IP layer. UDP takes messages from the application process, attaches source and destination port number fields for the multiplexing/demultiplexing service, adds two other small fields, and passes the resulting segment to the network layer. 

- `Connectionless`: No handshaking between sender and receiver. Often used for `real time`, `low delay`, and `low overhead` applications.
- Some applications are better suited for UDP
  - Allows `finer control over data sent and timing`.
  - `No connection establishment`, minimizing delays.
  - `No connection state,` supporting more active clients.
  - `Small packet header` overhead (UDP's 8 bytes vs. TCP's 20 bytes).  
- Reliability can be added to applications using UDP like QUIC protocol, but it's nontrivial. It can be built directly into the application.
- Allows reliable communication without TCP's congestion control limitations.
- Key fields in the UDP header:
  - `Port numbers`: For demultiplexing.
  - `Length`: Specifies the segment length (header + data).
  - `Checksum`: Used for error detection.
- Checks for alterations during data transmission.

    <img src="https://lh3.googleusercontent.com/pw/ADCreHccqsKMoJTpHKrpeBpWY5ePn7ro94y-9gTfw5NPXZ4IInxs2ZdGrHqi441xgHndC9vwiDPl3x3As6aVZTs6GQWNAMmBZTMwvHlIoT1R3MRvymYK7XqkB1O-OEWd8JhmP4Cm_f_nrzKGJwPARpdRqcQ=w1316-h1088-s-no" width="450" height="350">

> UDP at the sender side performs the 1s complement of the sum of all the 16 bit words in the segment, with any overflow encountered during the sum being wrapped around.

<img src="https://lh3.googleusercontent.com/pw/ADCreHd6aGmd6Jk9aEfaOuteJHdj1V8Tl3M-w_eAdWjDwwqOUuDR8hobSh1fjb2PyblDTqlzm8bLz72502F7YGVJF2x5nirudlaEPwHHrIdqbkWzDpvPUb6K3jccQN5bxYKKsbptwUDTjAnvI0uhICFYGpRv=w1286-h1130-s-no" width="550" height="500">

- Thus, the 1s complement of the sum `0100101011000010` is `1011010100111101`,

> At Receiver, all the four 16 bits (3 + checksum) are added, If no errors are introduced into the packet, then clearly the sum at the receiver will be 1111111111111111. If one of the bits is a 0, then we know that errors have been introduced into the packet.

> It is useful for the transport layer to provide error checking as a safety measure. Although UDP provides error checking, it does not do anything to recover from an error. Some implementations of UDP simply discard the damaged segment; others pass the damaged segment to the application with a warning.

### 3.6.5 Go-Back-N (GBN)

Animation: [Go-Back-N ARQ](https://www2.tkn.tu-berlin.de/teaching/rn/animations/gbn_sr/)


<img src="https://lh3.googleusercontent.com/pw/ADCreHf6riQ0xiX1Y8x0IaZhnnaUd6EYEaffccwXfQry67IIKawSascIKFG6Md8mSFxQh_g33BxvYHcKuYAEE2U9AlpXm-r64b5UlepEhonQYufEGA4w63KF1rhgAlaSNo4jzfsUfamxAi-tT4kk0VtgR3Cj=w1920-h440-s-no" width="750" height="200">

**Go-Back-N (GBN) ARQ Protocol**

---

### **Purpose**

A reliable data transfer protocol (Transport/Data Link layer). It ensures ordered, error-free delivery of packets over unreliable channels.

---

### **How it Works**

1. **Sender Side**

   * Maintains a **window of size N** (can send up to N unacknowledged frames).
   * Frames are numbered using **sequence numbers**.
   * Sender keeps transmitting new frames as long as window isn’t full.
   * If an ACK is not received for the oldest unacknowledged frame within timeout:
     → **Sender retransmits that frame and all frames after it** (hence "Go-Back-N").

2. **Receiver Side**

   * Uses **cumulative acknowledgment**.
   * If frame is received in order:

     * It delivers it to the upper layer.
     * Sends **ACK for that frame (or highest in-order frame)**.
   * If an **out-of-order frame** arrives:

     * Receiver discards it (does not buffer).
     * Re-sends ACK for the **last correctly received in-order frame**.

---

### **Key Points**

* **Efficiency**: Better than Stop-and-Wait, since multiple frames are in-flight.
* **Drawback**: If one frame is lost, all subsequent frames are retransmitted (wasted bandwidth).
* **Window size**: ≤ (2^m – 1), where *m* = number of bits in sequence number field.

---


### **Interview one-liner**

> Go-Back-N is a sliding window protocol where the sender can transmit multiple frames without waiting, but on error it retransmits the lost frame and all subsequent frames, while the receiver only accepts in-order frames and uses cumulative ACKs.

---

### 3.6.6 Selective Repeat (SR)

Animation: [Selective Repeat ARQ](https://www2.tkn.tu-berlin.de/teaching/rn/animations/gbn_sr/)

- **Performance Issues with GBN:**
  - GBN allows the sender to fill the pipeline with packets but can suffer from performance problems, especially when the window size and bandwidth-delay product are large.
  - A single packet error can trigger unnecessary retransmissions, potentially filling the pipeline with these redundant packets.
  - Selective-repeat protocols aim to avoid unnecessary retransmissions by having the sender retransmit only suspected lost or corrupted packets.
  - In SR, the sender can receive ACKs for some packets in the window, unlike GBN.


---


### **Purpose**

Reliable, efficient data transfer over unreliable channels — like GBN but smarter:
Instead of retransmitting *all* frames after a lost one, it **only retransmits the erroneous/lost frame**.

---

### **How it Works**

#### **Sender Side**

* Maintains a **window of size N**.
* Can send multiple frames without waiting (as in GBN).
* Keeps track of each unacknowledged frame individually.
* If a frame times out → **only that frame is retransmitted**.

#### **Receiver Side**

* Accepts **out-of-order frames** (unlike GBN).
* Buffers them until the missing frame(s) arrive.
* Sends **individual ACKs** for each correctly received frame.
* When missing frames arrive, buffered frames can be delivered in-order to the upper layer.

---

### **Key Differences: SR vs GBN**

| Feature              | Go-Back-N (GBN)           | Selective Repeat (SR)    |
| -------------------- | ------------------------- | ------------------------ |
| Receiver buffer      | No (discard out-of-order) | Yes (store out-of-order) |
| ACK type             | Cumulative ACK            | Individual ACK per frame |
| Retransmission       | From lost frame onwards   | Only lost frame          |
| Bandwidth efficiency | Lower                     | Higher                   |
| Complexity           | Simple                    | More complex             |



### **Window Size Rule**

For SR, to avoid confusion (duplicate frames being mistaken as new ones),
👉 **Window size ≤ 2^(m-1)**,
where *m* = number of bits in sequence number.

(GBN allows up to 2^m – 1).


## 3.7 TCP (Transmission Control Protocol)



* A **connection-oriented**, **reliable**, **byte-stream** transport protocol used on top of IP.
* Ensures data is delivered **in-order, without loss, duplication, or corruption**.
* Used by applications that require reliability (HTTP, HTTPS, FTP, SMTP, IMAP, etc.).

---

### **Key Features**

1. **Connection-oriented**

   * Requires a **3-way handshake** (SYN, SYN-ACK, ACK) before data transfer.

2. **Reliable delivery**

   * Uses **ACKs, sequence numbers, retransmissions, and timers**.

3. **Flow control**

   * Uses a **sliding window** to avoid overwhelming the receiver.

4. **Congestion control**

   * Adapts to network conditions using **algorithms (Slow Start, AIMD, Fast Retransmit, Fast Recovery)**.

5. **Full duplex**

   * Data can flow in both directions simultaneously.

6. **Byte-oriented**

   * Application sends a **byte stream**, TCP segments it, but delivery is seen as a continuous stream.

---

### **Structure of TCP Segment**

* **Header fields:**

  * Source Port, Destination Port
  * Sequence Number, Acknowledgment Number
  * Flags (SYN, ACK, FIN, RST, PSH, URG)
  * Window size (for flow control)
  * Checksum (for error detection)

---

- **TCP Segment Structure:**
  - A TCP segment consists of `header` fields and a `data` field.
  - Key fields include `source port` and `destination port`, `checksum`, `sequence number`, `acknowledgment number`, `receive window`, `header length`, and `flags`.
  - An options field can be included for features like maximum segment size (MSS) negotiation and window scaling.
  
  <img src="https://lh3.googleusercontent.com/pw/ADCreHcSNDV-yVd1BdDU6Nj4ezCL_1_VjcuUWaPSqFQBBYShSAwrC9jlbpw_LlvY8oITjDuOttW31BPxO9ayFockAc8Z9RjoVpQB9ai8_Sem2JD7fyJrLw32MmKF15kWA5VdEYtQSpshhgcUYFYip4ICJUY=w1406-h1130-s-no" width="530" height="400">


- **Sequence Numbers and Acknowledgment Numbers:**
  - Sequence numbers are assigned to bytes in the data stream and are included in the segment header.
  - Acknowledgment numbers represent the `next expected byte` in the opposite direction of data flow.
  - TCP uses `cumulative acknowledgments`, acknowledging the last byte received.
  - Handling out-of-order segments is left to TCP implementation and may involve discarding or waiting for missing bytes.

  


### 3.7.3 Flow Control

Animation: [Flow Control](https://www2.tkn.tu-berlin.de/teaching/rn/animations/flow/)

TCP Flow Control ensures that the sender doesn't overwhelm the receiver's buffer. When data arrives at the receiver, it's placed in a receive buffer, which the application reads from. If the application reads slowly, the sender can easily overflow the buffer.

- **Flow Control vs. Congestion Control:**
  - Flow control matches sender rate to receiver reading speed.
  - Congestion control manages sender rate due to network congestion.
  - Although they both throttle the sender, they serve different purposes.

- **TCP Flow Control:**

    <img src="https://lh3.googleusercontent.com/pw/ADCreHdwuKcHW7WDAFNgV855UgY1P66rxQ52f8nFf1Czx7h1J2gZoP60wVYzQRbXRwM6ooQbGPuL0WQxy2XKUZHWMPCoeRNV4p-vCd_dQv9AEn_dxAZ3SxIifgzty24DQQVfFs0ZOvasX8PyUvRoGx3TCfM=w1748-h860-s-no?authuser=2" width="400" height="250">

  - The sender maintains a `receive window variable (rwnd)` to determine available buffer space at the receiver.
  - Full duplex communication means both sender and receiver have `distinct receive windows`.
  - rwnd is `dynamic`, and Host B informs Host A by including rwnd in its segments.
  
  ```
  rwnd = RcvBuffer - [LastByteRcvd - LastByteRead]
  ```


---

### **How it Works**

1. **Receiver buffer**: Receiver allocates buffer space for incoming data.
2. **Advertised window**: Receiver sends back an **advertised window size** (rwnd) in ACKs.

   * Example: If buffer = 5000 bytes, and 2000 bytes are already filled → rwnd = 3000.
3. **Sender restriction**: Sender can send only up to **min(cwnd, rwnd)** bytes unacknowledged.

   * `cwnd` = congestion window (network capacity).
   * `rwnd` = receiver window (receiver capacity).
4. If **rwnd = 0**, sender must pause and occasionally send **probe packets** until receiver updates rwnd > 0.

---





### 3.7.4 TCP Connection Management

<img src="https://lh3.googleusercontent.com/pw/ADCreHerZiPLvIkD639YmnLg4pvsWFpC001vHpsgwfcRnyxsT3JyaW9A4xcLw2SoQIAR4qV6y-8JQ4eMA3WRWUse594rU-mnBwuK6xjDGe5kkqb6JVi7vKdf6pkWXMIDKO0Cr6iuuLM0Pak4vNxgMsWs7_M=w1920-h888-s-no?authuser=2" width="950" height="550">


### 🔹 Why Not **2-Way Handshake**?

Imagine if we only had:

1. Client → Server: **SYN** (I want to connect)
2. Server → Client: **ACK** (Okay, let’s connect)

❌ Problem:

* The **client cannot be sure** the server is ready (buffer allocated, connection state established).
* Old/delayed duplicate SYN packets could create **half-open connections** (server thinks connected, client doesn’t).

So **2-way handshake** is unreliable.



### 🔹 Why **3-Way Handshake**?

Steps:

1. **SYN** (Client → Server): Client says “I want to connect. My seq = X.”
2. **SYN-ACK** (Server → Client): Server says “Got it. I also want to connect. My seq = Y, and I ACK your X+1.”
3. **ACK** (Client → Server): Client confirms “I got your Y, and I’m ready.”

✔ Guarantees:

* Both **sides agree on sequence numbers** (initial seq exchange prevents old packets from interfering).
* Both confirm **each other’s readiness** (buffers, state, etc.).
* Prevents **half-open connections**.


### 🔹 Why Not **4-Way Handshake**?

Technically possible, but unnecessary.

* A 4th step (extra ACK from server) adds overhead without benefit.
* After the **third ACK**, both client and server already know the other is ready.

So, **3 is the minimum safe number**.

## 3.8 Congestion Control
 

### 🔹 What is Congestion?

* **Congestion** happens when **too many packets are injected into the network** and the **demand for resources (bandwidth, buffer, CPU) exceeds capacity**.
* Think of it like a **traffic jam on a highway** → too many cars, not enough lanes → everyone slows down.

📌 Example:
If multiple users download videos at once, the router’s **buffer fills up**, packets are dropped, retransmissions happen, and the network performance degrades.

---

### 🔹 Symptoms of Congestion

* **High delay** (packets wait in queues).
* **Packet loss** (buffer overflow in routers).
* **Retransmissions** (worsens congestion further → congestion collapse).
* **Throughput decreases** instead of increasing (network chokes).

---

### 🛠️ **Congestion Control Techniques**

Congestion control aims to **prevent congestion** (proactive) or **recover from congestion** (reactive).

---

### 1️⃣ **Open-Loop Control (Prevention, No Feedback)**

* Decisions are made at the **source** without feedback from the network.
* Example methods:

  * **Traffic shaping** (e.g., *Leaky Bucket*, *Token Bucket*).
  * **Admission control** (deny new connections if load is high).

---

### 2️⃣ **Closed-Loop Control (Feedback-based)**

* Network provides **feedback** about congestion → sources adjust sending rate.
* Example feedback: Explicit (bit in packet header) or Implicit (packet loss, delay).

---

## 3️⃣ **Techniques Used in Practice**

- **TCP Congestion Control Algorithm**
    
### 🔹 Key Phases 

1. **Slow Start**

   * `cwnd` begins at **1 MSS**.
   * Doubles each RTT (exponential growth).
   * Continues until **ssthresh** (slow start threshold).

2. **Congestion Avoidance**

   * Once `cwnd >= ssthresh`, growth becomes **linear** (increase by 1 MSS per RTT).

3. **Packet Loss Handling**

   * TCP Reno distinguishes **two types of packet loss detection**:

   **(a) Triple Duplicate ACKs (Fast Retransmit + Fast Recovery)**

   * If 3 duplicate ACKs are received → packet loss assumed.
   * Instead of dropping `cwnd` to 1 (like Tahoe), Reno does:

     * `ssthresh = cwnd / 2`
     * `cwnd = ssthresh` (halves, instead of restarting).
     * Retransmit the lost packet immediately.
     * Enters **Fast Recovery** (avoids going back to Slow Start).

   **(b) Timeout**

   * If ACK doesn’t arrive → timeout.
   * This is considered a **severe loss**.
   * `ssthresh = cwnd / 2`
   * `cwnd = 1 MSS` → restart with Slow Start.


    > TCP Tahoe, unconditionally cut its congestion window to 1 MSS and entered the slow start phase after either a timeout indicated or triple duplicate ACK indicated loss event. The newer version of TCP, TCP Reno, incorporated fast recovery.

    <img src="https://lh3.googleusercontent.com/pw/ADCreHfOLql8zoOonXOmIYdDXSO1lR3sBlmC5onGe2wHtLP4czHe02kSgwFNjVnJyYM9wpI3Ycw7WGUuaFGEdXiSnE9EULNAue-yJlaEfMLU8R8EjPf379tcqPvSpv86k-Qu3Xu2CVQdgo94ETgsx9IjNTI=w1768-h1094-s-no?authuser=2" width="600" height="400">

    TCP's congestion control exhibits `saw tooth` behavior, referred to as `additive increase, multiplicative decrease` **(AIMD)**. AIMD aims to simultaneously optimize user and network performance, probing for available bandwidth in an asynchronous manner.




## 🌐 Network-Assisted Congestion Control

### 🔹 Definition

In **network-assisted congestion control**, the **network (routers/switches)** actively participates in detecting and controlling congestion, instead of leaving it entirely up to the sender and receiver (end-hosts).
The routers provide **feedback** to end systems about the state of the network.

---

## 🔹 Why Needed?

* End-to-end (like TCP Reno) relies on **packet loss or delay** as implicit signals.
* This is **slow and wasteful** because:

  * Packets get dropped before sender detects congestion.
  * Retransmissions increase congestion further.

👉 With network assistance, routers can **proactively signal congestion**, avoiding packet loss.

---

## 🔹 Mechanisms of Network-Assisted Congestion Control

1. **Choke Packets**

   * Router explicitly sends a special control packet to the sender indicating congestion.
   * Example: **ICMP Source Quench (deprecated now)**.

2. **Explicit Congestion Notification (ECN)**

   * Modern technique (used with TCP).
   * Instead of dropping packets, routers **mark packets** with a congestion bit (ECN bit in IP header).
   * Receiver notifies sender → sender reduces sending rate.
     
<img src="https://lh3.googleusercontent.com/pw/ADCreHdgekG0rBZ1X-scpp5eaH2nUlJLL8xjB0dn958V8M8MBapJ46_dUNdkB-nqR__S6m142ELWrX-QJ7ytpicpWKDSYooKp5y3_lqADmCP-wFgjxEfuYuL4K_bLKdYfDtJ-51tZ0k_RNTaf8uO553bckQ=w910-h496-s-no?authuser=2" width="550" height="300">

3. **Hop-by-Hop Backpressure**

   * Router experiencing congestion tells its **upstream router** to slow down, and so on, until the source slows.
   * Used in virtual circuit networks (like ATM).

4. **Fair Queuing / Scheduling in Routers**

   * Routers can schedule packets fairly (e.g., round-robin per flow) instead of letting one greedy sender dominate.
   * Example: **Weighted Fair Queuing (WFQ)**.

---


---

## 🔹 Comparison

| Aspect               | End-to-End (TCP Reno etc.) | Network-Assisted (ECN, Choke)      |
| -------------------- | -------------------------- | ---------------------------------- |
| Congestion Detection | Implicit (loss/delay)      | Explicit (router signals)          |
| Reaction Speed       | Slower                     | Faster (before packet loss)        |
| Router Involvement   | None                       | High (mark/drop packets, feedback) |
| Used In              | Internet TCP               | ATM, Frame Relay, modern TCP-ECN   |



## 🔹 What is QUIC?

**QUIC (Quick UDP Internet Connections)** is a **transport layer protocol** developed by **Google** and later standardized by the **IETF**.
It’s designed to replace **TCP + TLS + HTTP/2** stack with a **faster, secure, and more reliable protocol** built **on top of UDP**.

👉 QUIC = UDP + Reliability + Security + Multiplexing + Congestion Control.

---

### 🔹 Why QUIC was created?

Traditional **HTTP/2 over TCP + TLS** had problems:

1. **TCP Handshake + TLS Handshake = Slow Start** (extra round-trips).
2. **Head-of-Line Blocking**: In HTTP/2, if one stream stalls, all streams over that TCP connection are blocked.
3. **Middleboxes** (NATs, Firewalls) interfere with TCP options, making innovation hard.
4. **Migration issues**: TCP connections break if IP/port changes (e.g., switching from Wi-Fi to mobile data).

👉 QUIC solves these by running over **UDP**, which is more flexible.

---

### 🔹 Features of QUIC

1. **Zero Round Trip Time (0-RTT) Handshake**

   * Combines **transport handshake (TCP 3-way)** and **TLS 1.3 handshake**.
   * Secure session can be established in **1 RTT** or even **0 RTT** (if session resumption).
   * Faster than TCP+TLS.

2. **Multiplexed Streams without Head-of-Line Blocking**

   * Independent streams in one QUIC connection.
   * If one packet is lost, only that stream waits, not others (unlike HTTP/2 over TCP).

3. **Built-in Encryption**

   * QUIC integrates **TLS 1.3**.
   * Encryption is mandatory → no insecure version like plain TCP.

4. **Connection Migration**

   * Connections are identified by a **Connection ID** (not IP+port).
   * If user switches from Wi-Fi → Mobile data, QUIC continues without reconnecting.

5. **Better Congestion Control**

   * Supports TCP-like algorithms (CUBIC, Reno, BBR).
   * Since it’s in **user space** (not OS kernel), it’s easier to update.

6. **Forward Error Correction (Optional)**

   * Can recover some losses without retransmission (though not always used).

---

### 🔹 Comparison: QUIC vs TCP+TLS+HTTP/2

| Feature              | TCP + TLS + HTTP/2       | QUIC                         |
| -------------------- | ------------------------ | ---------------------------- |
| Transport protocol   | TCP                      | UDP                          |
| Handshake RTTs       | 2–3 RTT                  | 1 or 0 RTT                   |
| Multiplexing         | Head-of-Line blocking    | No HoL blocking              |
| Security             | Optional (TLS over TCP)  | Mandatory (TLS 1.3 built-in) |
| Connection Migration | No (breaks on IP change) | Yes (via Connection ID)      |
| Deployability        | Kernel (slow updates)    | User space (fast updates)    |

---

### 🔹 Example in Real World

* Google Chrome, YouTube, Gmail, Facebook, and WhatsApp already use QUIC.
* **HTTP/3** is just **HTTP over QUIC** → That’s why HTTP/3 = QUIC + TLS 1.3.



