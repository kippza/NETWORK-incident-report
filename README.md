# NETWORK-incident-report


## Network Security Incident Report

## 1. Description of the Attack

The network experienced what appears to be a **Denial of Service (DoS)** attack. Specifically, it was a **SYN flood attack**, a type of DoS where an attacker sends a rapid succession of TCP SYN (synchronization) requests to a server in an attempt to overwhelm it.

#  Main Characteristics and Symptoms:
- High volume of incoming TCP SYN requests from a single IP address.
- Server became unresponsive and failed to load in a browser, resulting in **connection timeout errors**.
- The packet sniffer showed a large number of half-open TCP connections (incomplete three-way handshakes).
- Normal user traffic was blocked or severely delayed due to the attack.

---

# 2. Type of Attack and How It Works

This attack is a **TCP SYN flood**, a subset of DoS attacks. It exploits the **TCP three-way handshake** by initiating a large number of connections but not completing them. The server waits for the final ACK from the client that never arrives, leading to exhausted server resources.

**TCP handshake process:**
1. Client sends SYN.
2. Server responds with SYN-ACK.
3. Client should respond with ACK (but attacker never sends this).

In this case, only step 1 happened thousands of times, leaving the server waiting and consuming resources.

---

### **3. Impact on the Organization’s Network and Website**

- **Server Resource Exhaustion:** The server’s memory and connection table filled up with half-open connections.
- **Website Downtime:** Legitimate users (employees and customers) were unable to access the sales website.
- **Business Disruption:** Employees couldn’t search or recommend vacation packages to customers, directly affecting business operations and customer service.
- **Potential Reputation Damage:** Customers might view the downtime as a reliability issue, reducing trust in the agency’s digital services.

---

### **4. Difference Between DoS and DDoS**

- **DoS (Denial of Service):** A single system sends the traffic to overwhelm the target.
- **DDoS (Distributed Denial of Service):** Multiple systems (often botnets) simultaneously attack a single target, making it harder to block based on IP address alone.

In this scenario, **a single IP address** was the source, so it was likely a **DoS** attack. However, if similar traffic starts coming from multiple IPs, it could evolve into a DDoS.

---

### **5. Temporary and Long-Term Mitigation Measures**

**Temporary Action Taken:**
- Took the server offline to let it recover.
- Blocked the attacking IP address at the firewall.

**Limitations:**  
Attackers can easily **spoof IP addresses** or **rotate IPs** (in the case of a DDoS), rendering simple IP blocks ineffective.

---

### **6. Potential Consequences of the Attack**

- **Service Unavailability:** Loss of customer access to online services.
- **Loss of Revenue:** Employees unable to process sales during downtime.
- **Customer Dissatisfaction:** Reduced trust due to perceived instability.
- **Security Risks:** If part of a larger campaign, could lead to more serious intrusions.

---

### **7. Recommendations for Future Prevention**

To better protect the network from similar attacks in the future, consider the following:

#### **Technical Solutions:**
- **Rate Limiting:** Restrict the number of connection requests from a single IP.
- **Intrusion Detection and Prevention Systems (IDS/IPS):** Detect and block malicious traffic patterns.
- **SYN Cookies:** A TCP technique to handle SYN flood attacks without overloading resources.
- **Web Application Firewall (WAF):** Adds a layer of protection against traffic-based attacks.
- **Load Balancers:** Distribute traffic and help absorb attack loads.
- **Cloud-based DDoS Protection Services:** Like Cloudflare, AWS Shield, or Akamai, which filter malicious traffic before it reaches the server.

#### **Policy and Monitoring:**
- Regularly update firewall rules.
- Continuous monitoring of network traffic for anomalies.
- Security training for IT staff to identify early warning signs.

---

### **Conclusion**

The attack was a **TCP SYN flood DoS attack**, which overwhelmed the web server, making it unavailable to users. While a quick firewall block provided temporary relief, the attacker could return using spoofed IPs or distributed sources. To prevent future disruptions, it's critical to implement more advanced and layered security solutions.

