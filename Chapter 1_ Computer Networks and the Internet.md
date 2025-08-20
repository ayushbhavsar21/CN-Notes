# Chapter 1: Computer Networks and the Internet


A **computer network** is a system of interconnected computing devices that can communicate and share data, resources, and information with each other. These devices include computers, servers, printers, smartphones, routers, and other network-enabled equipment that are connected through physical cables (like Ethernet) or wireless connections (like Wi-Fi).[^2][^3][^7][^9]

## Key Components and Purpose

Computer networks enable devices to **exchange data using standardized communication protocols** such as TCP/IP, which govern how information is transmitted across the network. The primary purposes include:[^3]

- **Resource sharing**: Multiple devices can access shared printers, files, internet connections, and storage systems[^6]
- **Communication**: Enables email, video calls, messaging, and collaborative work[^6]
- **Data exchange**: Facilitates file transfers and information sharing between connected devices[^2]
- **Remote access**: Allows users to access network resources from different locations[^6]


## Types of Computer Networks

Networks vary in **size and scope**:[^5]

- **PAN (Personal Area Network)**: Connects personal devices like smartphones and laptops via Bluetooth
- **LAN (Local Area Network)**: Covers small areas like homes, offices, or schools
- **MAN (Metropolitan Area Network)**: Spans across a city or metropolitan area
- **WAN (Wide Area Network)**: Covers large geographical areas; the internet is the largest example


## How to Answer This in an Interview

When answering "What is a computer network?" in an interview, follow this structured approach:

### **Start with a Clear Definition**

"A computer network is a system where two or more computers and devices are connected to share data, resources, and communication using wired or wireless connections."[^6]

### **Explain the Purpose**

Mention the key benefits: "Networks enable file sharing, internet access, resource sharing like printers, and remote communication, which improves efficiency and reduces costs."[^6]

### **Give Examples**

"Networks can range from small home networks connecting a few devices to large-scale networks like the internet that connects billions of devices globally."[^3]

### **Mention Key Components**

"Networks use communication protocols like TCP/IP to ensure devices can communicate effectively, and include hardware like routers, switches, and various transmission media."[^7][^3]

### **Show Practical Understanding**

For technical roles, you might add: "For example, when you type a website URL, your computer uses DNS to resolve the domain name to an IP address, then routes the request through multiple networks to reach the destination server."[^6]

This approach demonstrates both **theoretical knowledge and practical understanding**, which interviewers particularly value in technical roles at companies like TCS, Infosys, and other IT firms.[^6]
<span style="display:none">[^1][^10][^4][^8]</span>

<div style="text-align: center">⁂</div>

[^1]: https://en.wikipedia.org/wiki/Computer_network

[^2]: https://www.geeksforgeeks.org/computer-science-fundamentals/what-is-computer-networking/

[^3]: https://www.techtarget.com/searchnetworking/definition/network

[^4]: https://aws.amazon.com/what-is/computer-networking/

[^5]: https://byjus.com/govt-exams/computer-networks/

[^6]: https://prepinsta.com/interview-preparation/technical-interview-questions/computer-network/

[^7]: https://www.ibm.com/think/topics/networking

[^8]: https://www.interviewbit.com/networking-interview-questions/

[^9]: https://em360tech.com/tech-articles/what-computer-network-definition-types-examples

[^10]: https://www.geeksforgeeks.org/computer-networks/basics-computer-networking/


### 1.4.1 Home Access: DSL 

- The two most common broadband residential access types are **DSL** and **cable**.
- DSL is often provided by the local telephone company, acting as `both telco and ISP`.
- DSL connections involve DSL modems at homes communicating with a DSLAM at the telco's central office.
- DSL allows data and telephone signals to share the same line using frequency division multiplexing.
- Splitters at the customer's end and DSLAMs at the telco end manage signal separation.
- DSL offers varying transmission rates, both downstream and upstream, with the potential for high speed access.
- DSL access can be asymmetric, with different rates for downstream and upstream.
- Achievable rates may be lower due to distance, line quality, and provider limitations.
- DSL is best suited for short distances from the central office, typically within 5 to 10 miles.

<img src="https://lh3.googleusercontent.com/pw/AIL4fc8Mjg-m_XwafZaE4lRMp6fpu9DwIJgZkiExxghXGh9Qgxsim6HBe-fnkxqSo6HH8bP_kVqIlEti8LEkvk9E0hzqz0Z2aJ_SfQlOVK21jFqxO92JFJ_Iq5vBibrrl7OcXmegiq0N0dLzvQhKRgf0xcSt=w1920-h860-s-no" width="700" height="300">

### 1.4.2 Home Access: Cable 

- Cable Internet uses the existing cable TV infrastructure.
- Fiber optics connect the cable head end to neighborhood junctions, then coaxial cable reaches individual homes.
- Because both fiber and coaxial cable are employed in this system, it is often referred to as hybrid fiber coax (HFC).
- Cable Internet requires cable modems to connect to home PCs via Ethernet.
- The cable modem termination system (CMTS) turns analog signals from cable modems into digital format.
- Cable Internet has downstream and upstream channels; downstream typically has higher transmission rates.
- Cable Internet is a shared broadcast medium, leading to shared bandwidth.
- Simultaneous usage can reduce individual user rates, but Web surfing is less affected.
- The upstream channel is also shared, requiring a multiple access protocol to avoid collisions.

<img src="https://lh3.googleusercontent.com/pw/ADCreHfdQzhpcW3Nqdx6s9Q_Z5hjTLqeWEM9okcmdCuwfbBvUoPaEZ4n9cJw4rR8iMS4wxuMWCzvzSd_4JsilUCHJ906VUKs6ayT5EcW8mkt8PXaPpphzNAfghV24ssJjVHHY3DrBNzuB5XYRlWXl2JznOOK=w1920-h934-s-no" width="700" height="300">

### DSL (Digital Subscriber Line) vs Cable Internet

| Feature              | DSL                                                                                     | Cable                                                                               |
| -------------------- | --------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| Medium               | Uses **existing telephone lines (twisted-pair copper)**                                 | Uses **coaxial cable** (same as cable TV)                                           |
| Bandwidth Sharing    | **Dedicated line** from your home to the telco office → speed not affected by neighbors | **Shared bandwidth** among users in the neighborhood → speed can drop at peak times |
| Speed                | Typically slower, ranges **1–100 Mbps** depending on DSL type (ADSL, VDSL)              | Faster, ranges **100 Mbps–1 Gbps**                                                  |
| Latency              | Higher latency                                                                          | Lower latency, better for gaming/streaming                                          |
| Distance Sensitivity | Speed drops as distance from telephone exchange increases                               | Less affected by distance (coax is more stable)                                     |
| Availability         | Works wherever phone lines exist (good rural coverage)                                  | Needs cable TV infrastructure (mostly urban/suburban)                               |

---



### 1.4.3 Home Access: FTTH 

**FTTH (Fiber to the Home)** = fiber-optic communication technology where a **fiber cable runs directly from the ISP to the end-user’s home**.

### Explanation

* Uses **optical fiber** instead of copper (DSL) or coaxial (cable).
* Provides **very high bandwidth** (up to 1–10 Gbps).
* Supports **symmetrical speeds** (upload ≈ download).
* Immune to electromagnetic interference, less signal loss over distance.
* Often deployed using **PON (Passive Optical Network)** or **Active Ethernet**.

### How it Works

1. ISP central office has an **OLT (Optical Line Terminal)**.
2. Fiber runs to local splitters (no power needed → passive).
3. From splitter, fiber runs directly into user’s home, terminating at an **ONT/ONU (Optical Network Terminal/Unit)**.
4. ONT converts optical signals into electrical signals for routers, Wi-Fi, etc.

### Advantages

* Very high speeds, future-proof.
* Stable and reliable connection.
* Better for video streaming, cloud apps, gaming.

### Short Interview Answer

> "FTTH, or Fiber to the Home, is a broadband access technology where optical fiber runs directly from the ISP to the customer’s home. It offers gigabit-level speeds, low latency, and high reliability compared to DSL or cable."



<img src="https://lh3.googleusercontent.com/pw/ADCreHfDt9ikXrQ0-2QZvqlKumBfhaRU9zh5meb36d0NOPJIinODENCl24OWvCxFxU_FUoMLI08IbvQ-Goz8aEDXwKgqzvfaXZiwa5biqMD0mD9Nhf7fprl9Gp3_emoohUaZmqKwOrufobgbJCbGEDJIJprt=w1808-h902-s-no" width="700" height="350">

### 1.4.4 Home Access: 5G Fixed Wireless

- 5G fixed wireless is an emerging technology for high speed residential access.
- It eliminates the need for **costly** and **unreliable cabling** from the telco's central office (CO) to homes.
- Data is sent wirelessly from a provider's base station to a modem in the home using beam forming technology.
- A WiFi wireless router is connected to the modem, similar to cable or DSL modem setups.

### 1.4.5 Enterprise & Home Access: Ethernet, WiFi

- Ethernet is the predominant LAN technology, using twisted pair copper wire with access speeds from 100 Mbps to tens of Gbps.
- Wireless LAN users connect to an access point, which is linked to the enterprise's network (usually via wired Ethernet).
- IEEE 802.11 (WiFi) is widely used for wireless LAN access with shared transmission rates exceeding 100 Mbps.
- Ethernet and WiFi are used not only in enterprise settings but also in home networks.
- Home networks often combine broadband residential access with wireless LAN technologies.

## 1.5 Physical Media

- Network access technologies in the Internet use various physical media, including fiber cable, coaxial cable, copper wire, and radio spectrum.

>  Physical media fall into two categories: guided media and unguided media. With guided media, the waves are guided along a solid medium, such as a fiber optic cable, a twisted pair copper wire, or a coaxial cable. With unguided media, the waves propagate in the atmosphere and in outer space, such as in a wireless LAN or a digital satellite channel.

- Installation labor costs for physical links can be significantly higher than material costs, motivating builders to install multiple types of media to save on future wiring expenses.
- **Twisted pair copper wire** is a common guided transmission medium, widely used in telephone networks and LANs. It consists of two insulated copper wires twisted together to **reduce interference**. Data rates for LANs range from 10 Mbps to 10 Gbps.
- Twisted pair technology, like category 6a cable, can achieve data rates of 10 Gbps for short distances, making it a dominant solution for high speed LAN networking.
- **Coaxial cable** consists of `two concentric copper conductors` and is commonly used in cable television systems. Coupled with cable modems, it provides high speed Internet access at rates of hundreds of Mbps.
- Coaxial cable can serve as a guided shared medium, allowing multiple end systems to connect directly to the cable and receive signals sent by other end systems.

> In cable television and cable Internet access, the transmitter shifts the digital signal to a specific frequency band, and the resulting analog signal is sent from the transmitter to one or more receivers.

- **Optical fibers** conduct light pulses as bits and offer high data rates, low attenuation, and resistance to interference.
- Fiber optics are ideal for long distance transmission but costly for short haul applications.

- **Terrsetial Radio channels** are wireless and versatile, influenced by propagation environment and distance.
- Three categories of terrestrial radio channels: `short range,` `local area`, and `wide area`.
- Radio channel characteristics include `path loss`, `shadow fading`, `multipath fading`, and `interference`.

- **Satellite communication** involves `geostationary` and `low earth orbiting (LEO)` satellites.
- Geostationary satellites stay fixed above one spot on Earth but introduce signal propagation delay.
- LEO satellites are closer to Earth, move in orbits, and may require multiple satellites for continuous coverage.
- Satellite links offer high speeds and serve areas without DSL or cable based Internet access.
- Satellite communication uses space-based relays to transmit voice, video, and data over long distances—for example, DTH TV, satellite internet in remote areas, GPS navigation, and disaster-recovery links.

## 1.6 Packet Switching (Store and forward Transmission)




Packet Switching is a method of transmitting data over a network where the message is **broken into small fixed- or variable-sized units called packets**. These packets are sent independently across the network and may take different routes to reach the destination, where they are reassembled into the original message.

This is the fundamental technique used in the **Internet (TCP/IP)**.

---

### 🔹 How It Works

1. **Message Division**

   * A large message (say an email or video stream) is divided into smaller packets.
   * Each packet typically contains:

     * **Header** → Contains source address, destination address, sequence number, error detection info, etc.
     * **Payload** → The actual data portion.
     * **Trailer (optional)** → Error checking (CRC).

2. **Independent Transmission**

   * Each packet is transmitted separately.
   * Routers/switches read the **header** to decide the best route.
   * Packets can take **different paths** through the network.

3. **Reassembly at Destination**

   * The receiving device collects packets.
   * Sequence numbers help reorder packets into the correct order.
   * Error-checking ensures no corruption (retransmission may occur if needed).

---

## 🔹 Types of Packet Switching

There are two main types:

### 1. **Datagram Packet Switching** (like the Internet – IP)

* Each packet is treated **independently**.
* No fixed path; routing decision is made per packet.
* Packets may arrive **out of order** or get **lost**.
* Example: **UDP (User Datagram Protocol)**.

👉 Analogy: Sending letters through a postal service. Each letter may take a different route.

---

### 2. **Virtual Circuit Packet Switching** (like ATM, Frame Relay)

* A **predefined logical path (virtual circuit)** is set up before data transfer.
* All packets follow the **same path** in order.
* More reliable and predictable than datagram method.
* Example: **TCP (Transmission Control Protocol)** uses virtual circuit concepts.

👉 Analogy: Making a phone call. A route is set up, and all conversation flows through it.

---

## 🔹 Example

Suppose you send this message:
**"HELLO"**

* Message is divided into 3 packets:

  * Packet 1: "HE"
  * Packet 2: "LL"
  * Packet 3: "O"

Each packet has a **header** (with source/destination, sequence number).
Packets may travel:

* Packet 1 → Route A
* Packet 2 → Route B
* Packet 3 → Route C

At the destination, packets are reordered using sequence numbers to form "HELLO".

---

## 🔹 Advantages of Packet Switching

✅ **Efficient use of bandwidth** – multiple users share the same channel.
✅ **Robust & fault-tolerant** – if one route fails, packets can take another path.
✅ **Scalable** – supports millions of simultaneous users.
✅ **Supports bursty traffic** – well-suited for modern Internet traffic.
✅ **Reduced transmission delay** for small messages.

---

## 🔹 Disadvantages of Packet Switching

❌ **Packet delay variation (jitter)** – since packets may take different routes.
❌ **Overhead** – extra header/trailer in each packet consumes bandwidth.
❌ **Packet loss** – possible during congestion.
❌ **Requires complex protocols** for reassembly and error handling.
❌ **Not ideal for real-time applications** without QoS (Quality of Service) support.

---

## 🔹 Packet Switching vs Circuit Switching

| Feature              | Packet Switching                           | Circuit Switching                        |
| -------------------- | ------------------------------------------ | ---------------------------------------- |
| Path                 | No fixed path (datagram) / Virtual circuit | Fixed path reserved before communication |
| Resource Utilization | Shared dynamically                         | Dedicated, reserved (may stay idle)      |
| Efficiency           | High (good for bursty data)                | Low (resources wasted if silent)         |
| Delay                | Variable (may reorder packets)             | Constant (once path established)         |
| Reliability          | Needs retransmission/error handling        | Very reliable, but inefficient           |
| Examples             | Internet (TCP/IP, UDP)                     | Telephone network                        |




<img src="https://networkencyclopedia.com/wp-content/uploads/2019/10/packet-switching.png" width="700" height="400">



## 1.7 Circuit Switching

> In circuit switched networks, the resources needed along a path (buffers, link transmission rate) to provide for communication between the end systems are reserved for the duration of the communication session between the end systems.

- Circuit switched networks reserve resources (buffers, link transmission rate) for the entire communication session, while packet switched networks use resources on demand and may involve queuing.
- Traditional telephone networks are examples of circuit switched networks, where circuits are established and transmission rate is reserved for the entire connection.
- **Multiplexing in circuit switched networks** can use `frequency division multiplexing (FDM)` or `time division multiplexing (TDM)`.

<img src="https://lh3.googleusercontent.com/pw/ADCreHcnymJYAUF4Fn1TBsyIZwgZJ6JIBFewHZxR1y6w26eel_YuQjD32j5gqkJZ-NqMjqr32WXra6HCaP_Z9-HXc6oKcrzDifgPrrmuGzS7ec1I4rjT_R5SEviCfBTv0nLAHwlFcVUsi1hTgfto2b6-cU4q=w1482-h1088-s-no" width="600" height="400">

>  FDM, the frequency domain is segmented into four bands, each of bandwidth 4 kHz. For TDM, the time domain is segmented into frames, with four time slots in each frame.

- Packet switching is seen as more efficient because it doesn't reserve resources during idle periods, while circuit switching does.
- Packet switching allows better sharing of transmission capacity and is simpler and more cost effective than circuit switching.
- Packet switching allocates link use on demand, while circuit switching pre allocates link use regardless of demand.

## 1.8 Networks of Networks

- **Network Structures:** Various network structures are discussed, including global transit ISPs, regional ISPs, and tier 1 ISPs.
- **Peering:** ISPs can peer, enabling direct traffic exchange without payment. Tier 1 ISPs also peer.
- **IXPs:** Internet Exchange Points facilitate ISPs' direct connections, enhancing efficiency.
- **Content Provider Networks:** Large providers like Google create their networks for control and cost reduction.

<img src="https://lh3.googleusercontent.com/pw/ADCreHfe3VrXVOkt6FxFDHy4qRsByO6EugEHMcLkEvVuXtz2Bz3iZW28h32W2rJs7faFriHzgxJIfbOPV2Gd5L1_0e9PqKnc_pCtjmqNN0OxeH15auTYBd17kowR13spgnTFSgBjINghCV3Ew7gDsBC8lIh5=w1920-h926-s-no" width="600" height="300">

## 1.9 Delay, Loss, Throughput



## 🔹 1. **Delay (Latency)**

The total time taken for a packet to travel from **source → destination**.

### Types of Delay:

1. **Propagation Delay**

   * Time for a signal to propagate through the medium.
   * Formula:

     $$
     D_{prop} = \frac{\text{Distance}}{\text{Propagation Speed}}
     $$
   * Example: 1000 km fiber link at $2 \times 10^8$ m/s → 5 ms.

2. **Transmission Delay**

   * Time to push all packet bits into the link.
   * Formula:

     $$
     D_{trans} = \frac{\text{Packet Size (bits)}}{\text{Transmission Rate (bps)}}
     $$
   * Example: 1 MB packet on 10 Mbps link → 0.8 s.

3. **Queuing Delay**

   * Time a packet spends waiting in router/switch buffers.
   * Varies depending on **traffic load**.

4. **Processing Delay**

   * Time taken by routers/switches to process header, check for errors, etc.
   * Usually microseconds.

👉 **Total End-to-End Delay**:

$$
D_{total} = D_{prop} + D_{trans} + D_{queue} + D_{proc}
$$

---

## 🔹 2. **Packet Loss**

* When a packet fails to reach its destination.
* Causes:

  * **Congestion** (buffer overflow in routers).
  * **Errors** (corrupted bits discarded).
  * **Timeouts** (lost during transmission).

👉 **Impact**: Requires retransmission (TCP handles this), increases delay, reduces throughput.

---

## 🔹 3. **Throughput**

* The actual **rate of successful data delivery** over a network (measured in bits/sec).

Types:

* **Instantaneous throughput** → At a given time.
* **Average throughput** → Over a longer duration.

Formula (basic):

$$
\text{Throughput} = \frac{\text{Total Data Received}}{\text{Total Time}}
$$

👉 Example: If 100 MB file is sent in 200 sec → Throughput = 0.5 MB/s ≈ 4 Mbps.

---

## 🔹 4. **Bandwidth**

* Maximum data rate supported by a link (capacity).
* Fixed by physical medium (e.g., fiber > copper).
* Measured in bits/sec.

👉 **Bandwidth ≠ Throughput**

* Bandwidth = potential capacity.
* Throughput = actual achieved speed (depends on loss, delay, congestion).

---

## 🔹 5. **Jitter**

* Variation in packet delay.
* Very important in **real-time applications** (VoIP, video conferencing).
* Low jitter → smoother audio/video.

---

## 🔹 6. **Goodput**

* Useful data delivered (excludes headers, retransmissions).
* More realistic than throughput.

$$
\text{Goodput} = \frac{\text{Application Data}}{\text{Total Time}}
$$

---

## 🔹 7. **RTT (Round Trip Time)**

* Time taken for a packet to go **source → destination → back**.
* Measured using `ping`.
* Important for TCP performance (affects congestion control, window size).

---

## 🔹 8. **Congestion**

* When demand > available capacity → queues build up, packets dropped.
* Causes:

  * Excessive traffic load.
  * Insufficient buffer size.
* Solutions:

  * **TCP Congestion Control** (slow start, AIMD).
  * **Active Queue Management (AQM)** like RED.

---

## 🔹 9. **Reliability**

* Ensuring data is **delivered accurately and in order**.
* Depends on:

  * Error detection & correction.
  * Retransmissions (ARQ in TCP).
  * Sequence numbers.

---

## 🔹 10. **Utilization**

* How effectively the link is being used.

$$
\text{Utilization} = \frac{\text{Throughput}}{\text{Bandwidth}} \times 100\%
$$

---

# 📊 Quick Comparison Table

| Term            | Meaning                                  | Unit     | Example  |
| --------------- | ---------------------------------------- | -------- | -------- |
| **Delay**       | Time taken to deliver data               | sec / ms | 50 ms    |
| **Packet Loss** | % of lost packets                        | %        | 2%       |
| **Throughput**  | Actual successful data rate              | bps      | 20 Mbps  |
| **Bandwidth**   | Max possible data rate                   | bps      | 100 Mbps |
| **Jitter**      | Delay variation                          | ms       | 5 ms     |
| **Goodput**     | Useful data only (excl. retransmissions) | bps      | 18 Mbps  |
| **RTT**         | Time for round trip                      | ms       | 200 ms   |
| **Utilization** | Link efficiency                          | %        | 80%      |





# 📘 Protocol Layers (1.11)

### 🔹 Protocol Layering

* Network communication is organized into **layers**.
* Each layer has a **specific role** and relies on the services of the layer below it.
* This modular approach makes design and troubleshooting easier.

---

### 🔹 Implementation of Layers

* **Software**: Higher layers (Application, Transport) are usually in software.
* **Hardware**: Lower layers (Physical, Data Link) are often in hardware.
* **Combination**: Some layers use both (e.g., Network layer in routers).

---

### 🔹 Advantages of Layering

✅ **Modularity** – easy to update or replace one layer without affecting others.
✅ **Simplicity** – provides a structured way to describe network functions.
✅ **Interoperability** – allows different technologies to work together.

---

### 🔹 Drawbacks of Layering

❌ **Duplication** – similar tasks (e.g., error checking) may appear in multiple layers.
❌ **Dependencies** – layers sometimes rely heavily on each other, reducing flexibility.

---

### 🔹 Protocol Stack

* A collection of protocols across all layers.
* **Internet Protocol Stack (TCP/IP model):**

  1. Physical Layer
  2. Link Layer
  3. Network Layer
  4. Transport Layer
  5. Application Layer

---

### 🔹 Encapsulation

* As data moves **down the stack**:

  * Each layer **adds its own header** (control information).
  * Forms a **packet** = \[Header + Payload].
* At the receiver side, headers are removed **layer by layer**.

👉 Example:
Message → \[App Hdr + Data] → \[Trans Hdr + …] → \[Net Hdr + …] → \[Link Hdr + …]



# 🔒 Networks Under Attack

* **Eavesdropping** – Unauthorized interception of data (sniffing).
* **Packet Injection / Modification** – Altering or inserting fake packets.
* **Denial of Service (DoS/DDoS)** – Overloading servers to make them unavailable.
* **IP Spoofing** – Faking source IP addresses to mislead systems.
* **Man-in-the-Middle (MITM)** – Attacker intercepts and manipulates communication.
* **Malware & Worms** – Infected programs spread across the network.

👉 **Goal**: Disrupt services, steal data, or compromise systems.

