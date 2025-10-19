>1. What is HTTP, and how does it work?
>    ● Definition: ○ HTTP (HyperText Transfer Protocol) is the foundation of communication on the web. ○ It enables the transfer of resources such as web pages, images, and API responses. 
>    ● How It Works: ○ A client (browser, mobile app, API client) sends an HTTP request to a web server. ○ The server processes the request and returns an HTTP response containing data or an error message. ○ The client receives the response and renders the requested resource (e.g., a webpage).
>     ● Example: ○ When you type https://www.example.com in a browser: ■ The browser sends a GET request to the web server. ■ The server responds with the HTML of the webpage. ■ The browser displays the webpage to the user.

>Why is HTTP considered a stateless protocol? 
>● Statelessness in HTTP: ○ HTTP does not retain memory of previous requests between the client and server. ○ Each request is treated as independent, meaning the server does not store session information. 
>● Challenges Due to Statelessness: ○ Maintaining user sessions (e.g., staying logged in). ○ Every request must include necessary information (e.g., authentication tokens). 
>● Solutions to Maintain State: ○ Cookies – Stored in the browser and sent with requests. ○ Sessions – Server-side storage of user data. ○ Tokens (JWT, OAuth) – Used for authentication and API security

>2. What are HTTP methods? 
>   When would you use PUT vs. PATCH? 
>   ● Common HTTP Methods & Use Cases: ○ GET – Retrieve a resource. ○ POST – Create a new resource. ○ PUT – Update an entire resource. ○ PATCH – Partially update a resource. ○ DELETE – Remove a resource. 
>   ● PUT vs. PATCH: Method Use Case Example PUT Replaces an entire resource Updating a user profile (name, email, password, etc.) PATCH Updates part of a resource, Changing only the email of a user without modifying the name



> How does TCP ensure reliability? 
   TCP guarantees reliable communication using the following mechanisms: 
   ● Three-Way Handshake: Establishes a connection before data transmission. 
   ● Acknowledgments (ACKs): Confirms receipt of packets. 
   ● Retransmission of Lost Packets: If a packet is lost, TCP resends it. 
   ● Error Checking: Uses checksums to detect corrupted packets. 
   ● Ordered Data Delivery: Reassembles packets in the correct order before passing them to the application.


---

## 1️⃣ Basic Questions

### **1. What is REST, and how does it differ from SOAP?**

**REST (Representational State Transfer)** is an **architectural style** that defines a set of constraints for designing web services. It primarily uses **standard HTTP methods** and focuses on **resources** rather than operations.

**Differences between REST and SOAP:**

|Aspect|REST|SOAP|
|---|---|---|
|Protocol|Architectural style|Strict protocol|
|Data Format|Typically JSON|XML|
|Performance|Lightweight and faster|Slower due to XML + WS-Security|
|Flexibility|Supports JSON, XML, HTML, etc.|XML only|
|Statefulness|Stateless|Can be stateful|

---

### **2. Six Constraints of REST Architecture**

1. **Client-Server Architecture** – Separation of concerns for scalability.
    
2. **Statelessness** – Each request contains all necessary info; no session state on server.
    
3. **Cacheability** – Responses can be cached to improve performance.
    
4. **Layered System** – System can be layered (e.g., security, load balancer) without client impact.
    
5. **Uniform Interface** – Standard HTTP verbs (GET, POST, PUT, DELETE).
    
6. **Code on Demand (Optional)** – Server can send executable code (e.g., JavaScript) to the client.
    

---

### **3. REST API vs. RESTful API**

- **REST API** → Follows _some_ REST principles.
    
- **RESTful API** → Fully compliant with _all six_ REST constraints.
    

---

### **4. What is a Resource in REST?**

- A **resource** is any object/entity accessible via the API (e.g., users, products).
    
- Represented by **URIs (Uniform Resource Identifiers)**.
    

**Examples:**

```
/users/{id}
/products/{id}
```

---

### **5. What are Endpoints in REST APIs?**

An **endpoint** is a specific URL where a client interacts with a resource.

**Examples:**

```
GET /users/{id}      → Retrieve user details
POST /orders         → Create a new order
```

---

## 2️⃣ HTTP Methods & Status Codes

### **6. HTTP Methods**

|Method|Description|Idempotent|
|---|---|---|
|**GET**|Retrieve data|✅ Yes|
|**POST**|Create new resource|❌ No|
|**PUT**|Replace entire resource|✅ Yes|
|**PATCH**|Partially update a resource|⚠️ Not always|
|**DELETE**|Remove a resource|✅ Yes|

---

### **7. PUT vs PATCH**

- **PUT** → Replace the _entire_ resource.
    
- **PATCH** → Update _specific fields_ only.
    

---

### **8. Common HTTP Status Codes**

|Code|Meaning|
|---|---|
|200|OK – Successful request|
|201|Created – Resource created|
|204|No Content – Success, no body|
|400|Bad Request – Invalid request|
|401|Unauthorized – Auth required|
|403|Forbidden – Permission denied|
|404|Not Found – Resource missing|
|500|Internal Server Error|

---

## 3️⃣ RESTful API Design & Best Practices

### **9. Best Practices**

✅ Use **plural nouns** for resources (`/users`, not `/user`)  
✅ Use **proper HTTP status codes**  
✅ Support **versioning** (`/v1/resources`)  
✅ Use **pagination** (`?page=2&limit=20`)  
✅ Implement **rate limiting**  
✅ Use **OAuth2 or JWT** for authentication

---

### **10. Example: Blogging Platform API**

|Endpoint|Description|
|---|---|
|GET /posts|Get all posts|
|POST /posts|Create a new post|
|GET /posts/{id}|Get a specific post|
|POST /posts/{id}/comments|Add a comment|

---

### **11. What is HATEOAS?**

**HATEOAS (Hypermedia as the Engine of Application State)** — API responses include links to relevant actions.

**Example:**

```json
{
  "id": 1,
  "name": "John",
  "links": {
    "self": "/users/1",
    "orders": "/users/1/orders"
  }
}
```

---

### **12. Authentication & Authorization**

✅ Use **OAuth 2.0** for authentication  
✅ Use **JWT (JSON Web Token)** for sessions  
✅ Implement **API Keys** for third-party access

---

## 4️⃣ Advanced & Real-World Questions

### **13. Caching in REST APIs**

Use HTTP headers:

```
Cache-Control: max-age=3600
ETag: "version-id"
```

---

### **14. Pagination**

Use query parameters:

```
GET /users?page=2&limit=10
```

---

### **15. Versioning**

|Method|Example|
|---|---|
|URI-based|/v1/resource|
|Header-based|Accept-Version: v1|
|Query-based|?version=1|

---

### **16. REST vs GraphQL vs gRPC**

|Feature|REST|GraphQL|gRPC|
|---|---|---|---|
|Data Format|JSON, XML|JSON|Protocol Buffers|
|Query Flexibility|Fixed endpoints|Custom queries|Strict methods|
|Performance|Medium|High|Very High|
|Use Case|General APIs|Complex data fetching|Low-latency services|

---

### **17. Improving REST API Performance**

✅ Enable **caching**  
✅ Use **gzip compression**  
✅ Implement **async processing**  
✅ Add **database indexing**

---

### **18. Can REST APIs be Stateful?**

No — REST should be **stateless**, though some implementations may use sessions (making them semi-stateful).

---

### **19. REST API Security**

- Use **parameterized queries** (prevent SQL injection)
    
- Use **CSRF tokens**
    
- Enforce **HTTPS**
    

---

## 5️⃣ Summary

- REST follows **6 constraints**: stateless, cacheable, client-server, uniform interface, layered system, and (optional) code-on-demand.
    
- Use **proper HTTP verbs** and **status codes**.
    
- Implement **security** (OAuth, JWT) and **performance optimization** (caching, pagination).
    

---