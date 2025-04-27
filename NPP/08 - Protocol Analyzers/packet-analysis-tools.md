# Packet Analysis Tools

This document covers two essential packet analysis tools—Wireshark and tcpdump—explaining their importance, basic usage, filtering techniques, and advanced command examples.

---

## Wireshark

**Why use Wireshark?**  
- Understand how protocols and communications work.  
- Identify network problems and performance issues.  
- Analyze exploits and attack traffic in detail.

### Display Filters
Wireshark allows you to apply filters by protocol, IP address, port, and more. You can combine expressions using `&&` in the filter bar.
- **Protocol filters**: `http`, `dns`, `tcp`, etc.  
- **IP filters**:  
  ```text
  ip.addr == 192.168.1.100   # Any packet with source or dest IP
  ip.src == 192.168.1.100    # Only packets from this IP
  ip.dst == 192.168.1.100    # Only packets to this IP
  ```
- **Port filters**:  
  ```text
  tcp.port == 80             # Any TCP packet using port 80
  ```

### Searching Payload Strings
- **TCP payload**:  
  ```text
  tcp contains "password"
  ```  
- **HTTP URI**:  
  ```text
  http.request.uri contains "/login"
  ```

---

## tcpdump

`tcpdump` is a command-line packet capture tool. Below are common use cases and filters.

### Basic Capture
- Capture all traffic on an interface and save to a file:  
  ```bash
  tcpdump -v -i eth0 -w capture.pcap
  ```
- Capture only a specific protocol (e.g., UDP):  
  ```bash
  tcpdump -v -i eth0 udp -w udp_capture.pcap
  ```

### Reading Captures
- Read and display packets from an existing file:  
  ```bash
  tcpdump -r capture.pcap
  ```
- Show numerical IPs instead of names:  
  ```bash
  tcpdump -nr capture.pcap
  ```
- Verbose output for more details:  
  ```bash
  tcpdump -vnr capture.pcap
  ```
- Include Ethernet frame details:  
  ```bash
  tcpdump -venr capture.pcap
  ```
- Combine protocol filter when reading:  
  ```bash
  tcpdump -vnr capture.pcap tcp
  ```
- Filter for traffic to or from a host:  
  ```bash
  tcpdump -vnr capture.pcap src host 10.0.0.5
  tcpdump -vnr capture.pcap src host 10.0.0.5 and dst host 10.0.0.6
  ```
- Filter by port number:  
  ```bash
  tcpdump -vnr capture.pcap port 443
  ```

### Advanced Output Processing
You can pipe `tcpdump` output to text-processing tools like `grep`, `cut`, `sed`, and `awk`.
- **Grep for a keyword**:  
  ```bash
  tcpdump -vnr capture.pcap | grep "Error"
  ```
- **ASCII payload view** (`-A` flag):  
  ```bash
  tcpdump -vnAr capture.pcap
  ```
- **Hex & ASCII view** (`-X` flag):  
  ```bash
  tcpdump -vnXr capture.pcap
  ```
- Flags appear in square brackets (`[S.]` for SYN-ACK, `[F.]` for FIN-ACK, etc.).

---

## Port Scan Analysis
Detect and analyze port scans using `tcpdump` and text tools.

1. Capture the first N lines:  
   ```bash
   tcpdump -vnr portscan.pcap | head -n 20
   ```

2. Extract source IPs and ports (remove TTL entries):  
   ```bash
   tcpdump -vnr portscan.pcap | cut -d " " -f5 | grep -v ttl
   ```

3. Filter FIN packets from a specific source host:  
   ```bash
   tcpdump -vnr portscan.pcap src host 10.0.0.5 \
     | cut -d "," -f1 \
     | grep -v tos \
     | grep -v "S" \
     | grep "F\."
   ```
---
