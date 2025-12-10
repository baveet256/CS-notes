


   Commands :  npm i -g (global installer flag) typescript
	This creates tsconfig file.
	
 `routes/user.ts` — maps URLs → controller functions  
✔ `controllers/user.ts` — contains logic, DB work, returns response  
✔ `models/user.ts` — defines MongoDB schema & model  
✔ Controller must send `res.json()`, `res.status()` etc.



## 📝 **Why OTP sending should be offloaded to a queue**

When a user logs in, the backend must generate and send an OTP (email/SMS).  
Sending the OTP is **slow** — it involves network calls to email/SMS providers and possible retries.  
If this work is done directly inside the controller, the API response becomes slow and blocks the request.

A better architecture is to **offload OTP sending to an asynchronous worker using a message queue** (RabbitMQ, Inngest, BullMQ, etc.):

1. **User hits `/login`**
    
2. Backend validates user
    
3. Backend pushes a job (email, OTP data) to the **queue**
    
4. Controller returns immediately
    
5. A separate **worker** receives the job and sends the OTP
    
6. Worker can retry on failures without blocking the API
    
7. OTP is also stored (DB/Redis) so backend can verify it later
    

This makes the login flow:

- faster
    
- more reliable
    
- scalable
    
- fault-tolerant (retries, dead-letter queue)
    

Queues decouple the **API logic** from the **slow background job** of sending OTP emails/SMS.

We use Amqblib in background to connect rabbitmq with the node

# ✅ Why a new service needs its own `tsconfig.json`

A **service** usually means:

- a different backend microservice
    
- a worker service (RabbitMQ consumer)
    
- a separate server
    
- any independent process
    

Each one usually has:

- its own source folder
    
- its own build output
    
- possibly different TypeScript settings
    
- its own `package.json` (optional but common)
    

Because of this, **TypeScript must know how to compile that service separately**, so it needs a `tsconfig.json`.


# 📝 **Login + OTP Flow with Redis + RabbitMQ + Mail Worker**

### 1️⃣ **Login Request**

- User submits email to backend (`POST /loginUser`)
    
- Controller logic:
    
    - Validate email
        
    - Generate random OTP (6 digits)
        
    - Store OTP in Redis with TTL (e.g., 5 minutes)
        
    - Publish OTP job to RabbitMQ (`send-otp` queue)
        

### 2️⃣ **Mail Microservice (Worker)**

- Listens on `send-otp` queue
    
- Receives job: `{ to, subject, text }`
    
- Sends email via Nodemailer
    
- Calls `channel.ack(msg)` **after email sent**
    

> ✅ Note: RabbitMQ `ack` only confirms message delivery; it does **not** verify OTP correctness.

### 3️⃣ **OTP Verification**

- Frontend collects OTP from user input
    
- Sends to backend (`POST /verify-otp`)
    
- Controller:
    
    - Fetch stored OTP from Redis (`otp:<email>`)
        
    - Compare input OTP with stored OTP
        
        - Match → login successful → optionally redirect to home
            
        - No match → return error
            
    - Delete OTP from Redis to prevent reuse
        

### 4️⃣ **Key Points**

- RabbitMQ is only for **asynchronous email delivery**
    
- Redis is the **single source of truth** for OTP verification
    
- Controllers remain fast — email sending does not block API response
    
- Rate-limiting and TTL ensure security and prevent brute-force







# Middleware

	We do isAuth, which verifies if request is authorized or not. so the request passes through middleware, which searches for bearer token in the request. jwt verify with the JWT SECRET KEY, if this is decoded or not, if yes, then proceed with whatever logic the endpoint is intended to have. 
	
	if not, then just return at any point of time here.
