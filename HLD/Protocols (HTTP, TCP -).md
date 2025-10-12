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