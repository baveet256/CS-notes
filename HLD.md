
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