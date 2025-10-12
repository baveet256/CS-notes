
>General Purpose - T series
	Compute Optimized : Batch Processing workloads, media transcoding, High performance web servers, High Performance Computing, Scientific modeling and Maching Learning, Gaming Servers (C name)
	
	Memory Optimized :  High performance for relational/ non relational, in memory Databases for BI, real time processing of big unstructured data (R series)
	
	Storage Optimzed : High frequency online transaction processing (OLTP) systems, relational and NoSQL databases, Cache for in memory databases, Data Warehousing applications, Distributed file systems (I/D/H1)
	

>Security Groups:  
	
	Can be attached to multiple instances, Locked down to a region/ VPC combination
	
	Does live "outside" the EC2 - if traffic is blocked the EC2 instance won't see it.
	
	It's good to maintain one seperate security group for SSH access
	
	if your application is not accessible, then it's a security group issue
  

	ports:
	
	SSH - port 22
	
	FTP - 21 file transfer protocol
	
	SFTP - 22 secure file transfer protocol
	
	HTTP - 80, Access unsecured websites
	
	HTTPS - 443 access secured websites
	
	RDP (remote desktop protocol) - 3389 log into a windows instance



>The EC2 instance gets **temporary credentials automatically** via the **Instance Metadata Service (IMDS)**.
>
	Any app inside the EC2 that uses the AWS SDK/CLI can automatically pick up those credentials and talk to S3 without you needing to configure access keys.
	
	Example:	
	1. You attach an IAM role with `AmazonS3FullAccess` to your EC2.
	    
	2. You SSH into the EC2.
	    
	3. Run:
	    
	    1. aws s3 ls
	    
	4. It works, even though you never did `aws configure` — because the role is providing temporary credentials.
	    
	
	IAM roles are **permission sets for AWS services** that you can attach to resources like EC2. Once attached, anyone using that resource can act with those permissions.

#TYPES

>On demand (For short term  and un-interrupted workloads) - billing per second, all other - billing per hour, highest cost and no upfront payment,  no long term .

>Ec2  Reserved  (For steady state usage applications) -  discounted than on demand, reserve a specific instance attribute if more time reserved then discount increases more. Payment option - No upfront - less discount, All upfront - Max discount

>Convertible Reserved Instance - can change EC2 instance type, instance family, OS, scope and tenancy

>EC2 Savings plan - locked to specific instance family and region (series and a region)

>EC2 Spot Instances (For workloads, resilient to failure, not for critical jobs) - can lose if user's max price is less than current spot price, the most cost efficient workloads

>EC2 dedicated Hosts (when compliance requirement or complicated licensing model , bring your own license (BYOL), most expensive)-

>EC2  dedicated Instances - Reserve On demand instances in a specific AZ for any duration


>>EC2 Spot Instances:

define max spot price, to get instance, if current spot price. < max spot price, get the instance

if current spot price > max spot price:

then you can stop or terminate instance with a 2 minutes grace period

  
SPOT Requests:

#### **One-time (default)**

- Request is fulfilled once.
    
- If instance is launched and later terminated (either by you or AWS), the request is **closed**.
    
- It won’t try again automatically.
    

Use this if you only need **cheap compute once** and don’t want auto-relaunch.

#### 2. **Persistent**

- Request **remains open** until you manually cancel it.
    
- If the instance is terminated by AWS (capacity reclaimed), the request will try to **launch a replacement instance** when capacity becomes available again.
    
- This is useful for workloads that can tolerate interruptions but should **resume automatically** when capacity is back.


>>>>SPOT Workflow

- You submit a **Spot Request**.
    
    - Specify instance type, AMI, VPC/subnet, max price (optional), and whether it’s **one-time** or **persistent**.
        
- AWS checks if there’s available spare capacity at or below your price.
    
    - If yes → AWS launches the instance.
        
    - If no → your request stays pending until capacity is available.
        
- If AWS needs the capacity back → they terminate your instance, but your request type (one-time/persistent) decides what happens next.
    

State Meaning :  **Open -** Waiting for capacity (not fulfilled yet). **Active -** Running instances are attached to the request. **Disabled -** Temporarily paused (no new launches). **Closed -** Fulfilled once and finished (can’t reopen). **Cancelled -** Request terminated by you, no new launches.

Canceling a Spot request doesnt terminate instances, and spot request can only be cancelled when they are open , active or disabled



>>- A **Spot Fleet** is a collection of **Spot Instances (and optionally On-Demand instances)** managed as a single unit.
    
- AWS automatically launches and maintains the fleet to meet **your target capacity**.
    

#### 🛠 Key Features

1. **Target Capacity**
    
    - Specify how many total vCPUs or instances you want.
        
    - AWS launches multiple instance types across Availability Zones to reach that target.
        
2. **Allocation Strategies**
    
    - **LowestPrice:** Launches instances in the cheapest AZs/instance types.
        
    - **Diversified:** Spreads instances across multiple AZs to reduce risk of interruption.
        
    - **CapacityOptimized:** Picks AZs least likely to be interrupted.
        
    - priceCapacityOptimised: pools with the highest capacity and then select pool with the lowest price
        
3. **Mix of Spot + On-Demand**
    
    - You can mix Spot + On-Demand to balance **cost vs reliability**.


#### SPOT FLEET WORKFLOW

1. Define fleet → specify target capacity, instance types, AZs, allocation strategy.
    
2. AWS launches instances to match your capacity.
    
3. Spot interruptions → fleet automatically replaces instances according to your strategy.
    
4. You can **update or scale** the fleet anytime.
    

✅ **In short:**

- Spot Fleet = **managed group of Spot (and optionally On-Demand) instances**.
    
- Automatically handles **launch, termination, replacement, and scaling** to maintain target capacity.


>**EC2 User Data** (a bootstrap script) to install software and update OS packages during the **first boot** of the instance.



>EC2 Placement group, specify strategies, like : Clusters - clusters instances into a low latency group in a single AZ (Low latency high throughput). Spread - spreads instances across underlying hardware (max 7 instances per group per AZ) - Critical Applications.

Partition Placement Group (your question)

- **Idea:** AWS divides the hardware into **partitions** (like logical racks). Each partition has its own set of racks, power, and networking. Each **partition** is isolated from failure
    
- When you launch EC2 instances in a **partition placement group**, AWS makes sure that **instances in different partitions don’t share the same underlying hardware**.
    
    Use case:
    
- Best for **big data workloads (Hadoop, HDFS, Cassandra, Kafka, etc.)**
    
- You can have up to **7 partitions per AZ**.