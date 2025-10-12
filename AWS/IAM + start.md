How to choose AWS region:  
  
compliance: a data cannot leave a particular region

Proximity: to reduce latency, nearby region is chosen

Available services : some service may not be available is one particular region

Pricing : Varies by region, so like choose whats the best for the business practice


>Each region has many availability zones, usually 3, max is 6. and each AZ is one or more discrete data center with power network and connectivity.  
	They seperate from each other, so that they are isolated from disasters
	They all are connected with each other with high bandwidth and ultra low latency networking


>Users can belong to multiple groups, and they work on least previledge principle, roles are the permissions.
>Add tags to give meta data to the resources.
	users inherit group permissions.


>IAM policies:
	if a user doesn't belong to a group : inline policy
	
	Json structure:
	
	    Version: policy language version, ID: identifies for the policy, Statement: one or more individual statements
	
	Statement also has a identifier, an Effect (allow or deny) , Principal (applicable to where/who), action (all actions user can do - Allow or Deny), resource (list of resources the actions can be applied)


>IAM roles: some AWS service will need you to perform actions on your behalf, to do so assign permissions to AWS services with IAM roles.

	EC2 instance roles, Lamda function roles.  
	like and EC2 instance role, can be a EC2 instance and if that needs to contact other AWS service, it will do it by the IAM role.
	
	IAM Security Tools -  IAM credentials report (Account level - a report that lists all your account's users and the status of their credentials ) and IAM access Advisor / Last Access (User level - shows service permissions granted to a user and when those services were last accessed, can be used to revise policies)



