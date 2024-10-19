# Analyzing a SYN Flood Attack
Analyzing a SYN Flood Attack: A Case Study

## Project Description
This project provides a detailed analysis of a Denial of Service (DoS) attack, specifically a SYN flood attack, that targeted a travel agency's web server. The analysis is based on Wireshark logs and offers insights into the attack's mechanics, potential impact, and recommended mitigation strategies.

## Key Technologies
Wireshark

## Project Structure
Wireshark Log Analysis
 - Overview
 - Technical Analysis
 - Recommendations

## Usage

Clone the Repository:   

git clone [https://github.com/InfosecWanderer/Analyzing-a-SYN-Flood-Attack.git]

**Review the Wireshark Logs:** Examine the captured network traffic in the wireshark_logs directory.

**Analyze the Incident Report:** Read the incident_report.md file for a detailed analysis of the attack and recommendations.

# Wireshark Logs

![Cybersecurity incident report - DOS Attack-images-1](https://github.com/user-attachments/assets/05bf2dcb-8491-48b2-8c55-3be84fdc24c0)

# Detailed Incident Analysis and Report:

## Section 1: Type of attack that may have caused this network interruption

One potential explanation for the website's connection timeout error message is likely a type of Network Attack known as a **Denial of Service (DOS) Attack**. 

A Network attack is an attempt to gain unauthorized access to an organization's network, with the objective of stealing data or performing other malicious activities. In this case, the attacker performed a malicious activity aimed to exhaust the Web server’s resources making it unavailable to legitimate users.

The logs show that the **Web server (203.0.113.0)** received over **70** multiple **TCP SYN requests** from the attacker’s system **(192.0.2.1)** in less than 5 seconds which could be high for the server to handle in such a short period, potentially overloading the server causing it to reject legitimate requests from users. 

**This event could be a Denial of Service (DOS) Attack**

**Denial of Service (DoS):** A DoS attack aims to disrupt the availability of a service to legitimate users by overwhelming the target system with a flood of illegitimate requests (TCP SYN requests in this case) or by exploiting vulnerabilities to crash the system. Typically, the attack originates from a single source, which might be a single machine or a small group of machines. This makes the system unavailable to real users. 

In the **CIA triad**, unavailability directly impacts one of the core information security goals: Availability.

The **CIA triad** refers to three fundamental principles for ensuring information security:

 - **Confidentiality:** Ensures information is only accessible to authorized users.
 - **Integrity:** Guarantees information remains accurate and unaltered.
 - **Availability:** Makes sure authorized users can access information and systems whenever needed.

If a system is unavailable, it means authorized users cannot access the information or resources they require, regardless of whether the information is confidential or remains unaltered. This disrupts workflows and can have significant consequences depending on the importance of the system.

A **Distributed Denial of Service (DDoS)**, is just like a DOS attack, but more **sophisticated**. It involves multiple compromised devices, often part of a botnet, flood the target with traffic simultaneously.

The employees of the company were unable to access the website because the Web server’s resources were exhausted and the server was overwhelmed with the requests limiting its ability to handle the load. As a result, the web server delays responding,  resets the SYN request and reports a connection timeout error message to the requesting user.

## Section 2: How the attack is causing the website to malfunction

When website visitors try to establish a connection with the web server, a three-way handshake occurs using the TCP protocol.

**1.**	First, the client sends a SYN (synchronize) packet to the server requesting a connection.
**2.**	The server responds with a SYN-ACK (synchronize-acknowledge) packet, acknowledging the request and sending its own synchronization data.
**3.**	Finally, the client sends an ACK (acknowledge) packet to complete the handshake and establish the connection.

When a malicious actor sends a huge amount of SYN packets all at once, it triggers a denial-of-service (DoS) attack known as a SYN flood attack. Here's how it works:

**1.	SYN Flood Attack:** In a SYN flood, the attacker sends a massive number of SYN packets to the server. However, the attacker intentionally doesn't respond with the final ACK packet.
**2.	Server Overload:** The server, overwhelmed by the SYN requests, allocates resources (memory and processing power) for each half-open connection. These connections wait for the non-existent ACKs from the attacker, effectively tying up valuable resources.
**3.	Denial of Service:** As legitimate clients try to connect, the server has depleted resources due to the backlog of half-open connections. This makes the server sluggish or unresponsive altogether, causing a DoS situation.

The DoS attack significantly disrupted the organization's website functionality and operations in several ways:

**Website Impact:**
●	Website Outage: The massive influx of traffic overwhelmed the web server, causing it to crash and become inaccessible to legitimate users.
●	Slow Performance: it becomes sluggish and unresponsive due to the strain on resources, before going off completely.
●	Loss of Revenue and Reputation: A DoS attack prevented potential customers from accessing the website, leading to lost sales or business opportunities. Additionally, the downtime and unreliability could damage the organization's reputation.
In essence, a DoS attack acts like a digital roadblock, flooding the network and website with junk traffic, preventing legitimate users from reaching their intended destination.

## Log Analysis:
The logs indicate the server is under a potential SYN flood attack, which is a type of Denial-of-Service (DoS) attack. Here's a breakdown of the log entries and how it affects the server:
Entries 63-68:
●	These lines show multiple SYN packets (green entries) sent from various IP addresses (198.51.100.5, etc.) to the server (192.0.2.1) on port 443 (HTTPS).
●	The server responds with SYN-ACK packets (red entries) acknowledging the requests and waiting for the final ACK from the clients to complete the connection handshake.
Entries 69-78:
●	Here, we see a pattern consistent with a SYN flood attack.
●	Multiple SYN packets (green entries) keep arriving from various IPs, but there are no corresponding ACK packets from the senders (missing green lines).
●	The server keeps sending SYN-ACK packets (yellow entries) but times out waiting for the final ACK (lines 77 and 80). This consumes server resources for each half-open connection.
Attack Impact:
●	This constant barrage of unanswered SYN requests ties up the server's resources (memory, processing power) because it waits for non-existent ACKs from the attackers.
●	This can slow down the server's response to legitimate connection requests (lines 71 and 79).
●	In severe cases, the server might exhaust resources and become unresponsive altogether, causing a complete DoS situation.
Log Breakdown Colors:
●	Green: Represents packets sent from the client (attacker or legitimate user) to the server.
●	Red: Represents packets sent from the server to the client.
●	Yellow: Represents the server's response to a legitimate connection attempt (successful handshake).
Overall, these logs show a potential DoS attack where the server is overloaded with unanswered connection requests, potentially impacting its ability to serve legitimate users.




