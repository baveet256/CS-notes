
## **What is DNS?**

- **DNS (Domain Name System)** is like the **phonebook of the internet**.
    
- Humans use domain names (e.g., `example.com`) but computers communicate via **IP addresses** (e.g., `93.184.216.34`).
    
- DNS **translates domain names into IP addresses** so your browser or application can connect to the right server.
    

---

## **How DNS Resolution Works**

When you type `www.example.com` in a browser, DNS resolution usually follows these steps:

### **1. Check Local Cache**

- First, your OS or browser checks if the IP for the domain is already **cached**.
    
- If found → use it → done.
    

---

### **2. Query Recursive Resolver (ISP or Public DNS)**

- If not cached locally, your request goes to a **recursive resolver** (e.g., your ISP’s DNS, or Google DNS `8.8.8.8`).
    
- Recursive resolver **knows where to ask** for the IP and handles the entire resolution process.
    

---

### **3. Root DNS Servers**

- If the resolver doesn’t know the IP, it asks a **root DNS server**.
    
- Root servers don’t know the exact IP but can point to the **TLD (Top-Level Domain) servers**.
    
- Example: For `www.example.com` → root server points to `.com` TLD server.
    

---

### **4. TLD (Top-Level Domain) DNS Server**

- The TLD server knows the authoritative DNS server for the domain.
    
- `.com` TLD server → points to **example.com’s authoritative DNS server**.
    

---

### **5. Authoritative DNS Server**

- This server **actually knows the IP address** of `www.example.com`.
    
- Returns the IP to the recursive resolver.
    

---

### **6. Return IP to Client**

- The recursive resolver sends the IP back to your **computer**.
    
- Your browser now connects to the server using that IP.
    
- The resolver and your OS usually **cache the IP** for some time (TTL) to speed up future requests.
    

---

## **Quick Flow Diagram**

```
Browser/OS Cache
        ↓
Recursive Resolver (ISP or 8.8.8.8)
        ↓
Root DNS Server
        ↓
TLD Server (.com, .org, etc.)
        ↓
Authoritative DNS Server (example.com)
        ↓
IP returned to browser
```

---

## **Additional Notes**

- **Caching:** Reduces latency and lowers DNS server load.
    
- **TTL (Time To Live):** How long the IP is cached.
    
- **Types of Records:**
    
    - **A record** → maps domain to IPv4
        
    - **AAAA record** → maps domain to IPv6
        
    - **CNAME** → alias for another domain
        
    - **MX** → mail server record
        

---

💡 **Analogy:**

- You want to call your friend “Alice.”
    
- You check your **phone cache** → if not found, you ask a friend (recursive resolver).
    
- Your friend checks the **directory service (root)** → points to the **local office (TLD)** → which has Alice’s **personal contact (authoritative server)** → and returns her number (IP) to you.
    

---

If you want, I can also explain **how DNS caching, propagation, and TTL interact**, which is very common in system design questions.

Do you want me to do that?

## Client Server Intraction

	Consists of synchonous vs Async

> What is a proxy server, and why is it used? 
	A proxy server is an intermediary system that sits between a client (such as a user's browser or device) and a destination server. When a client makes a request, the proxy server forwards it to the destination server, receives the response, and then relays it back to the client.
	
 >Why is a Proxy Server Used? 
	 A proxy server is primarily used for: ✅ Security & Privacy – It hides the client’s or server’s identity by masking IP addresses. ✅ Caching & Performance Optimization – Frequently requested content is stored and served faster. ✅ Traffic Control & Load Balancing – Helps distribute traffic evenly across multiple servers. ✅ Content Filtering – Blocks access to restricted or harmful content

>Explain the key differences between a forward proxy and a reverse proxy. 
>
	🔹 Forward Proxy ● Sits between clients and the internet – The client connects to the forward proxy, which then forwards the request to the target server. ● Used by clients to access external resources securely or anonymously. ● Common Use Cases: Hiding user identity, bypassing geo-restrictions, caching content. ● Example Tools: Squid Proxy, Shadowsocks, VPNs.
	🔹 Reverse Proxy ● Sits between users and backend servers – The user connects to the reverse proxy, which then forwards the request to an appropriate backend server. ● Used by servers to manage, secure, and optimize incoming traffic. ● Common Use Cases: Load balancing, caching, SSL termination, security (DDoS protection).● Example Tools: Nginx, HAProxy, Cloudflare, AWS Elastic Load Balancer.


> What is load balancing, and why is it important? 
>   
>   Answer: Load balancing is the process of distributing incoming network traffic across multiple backend servers to ensure efficient utilization, prevent overload, and improve system availability. ● Ensures High Availability: Prevents system downtime by redirecting traffic in case of server failure. ● Optimizes Resource Utilization: Spreads requests evenly to avoid overloading a single server. ● Improves Performance: Reduces latency by routing traffic to the best-performing server. ● Enhances Scalability: Supports horizontal scaling by adding more servers as demand grows. ● Increases Fault Tolerance: Redirects requests if a server fails, ensuring system reliability.

>  Explain the difference between Layer 4 and Layer 7 load balancing. 
>   
>   Answer: Layer 4 Load Balancing (Transport Layer) ● Operates at the network transport level (TCP/UDP). ● Distributes traffic based on IP addresses and port numbers without inspecting request content. ● Faster and more efficient for simple traffic distribution. ● Examples: AWS Network Load Balancer (NLB), HAProxy (L4 Mode). 
>   Layer 7 Load Balancing (Application Layer) ● Works at the application level (HTTP/HTTPS). ● Routes requests based on content, headers, cookies, or URL paths. ● Supports advanced features like SSL termination, caching, and authentication. ● Examples: AWS Application Load Balancer (ALB), Nginx, Traefik. Key Difference: Layer 4 is faster but less flexible, while Layer 7 is intelligent but adds overhead

>

