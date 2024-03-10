Stateful applicaton.
==

- MyClothes.com allows people to buy clothes online.
- There's a shopping cart
- Our website is having hundreds of users at the same time
- We need to scale, maintain horizontal scalability and keep our web
application as stateless as possible
- Users should not lose their shopping cart
- Users should have their details (address, etc) in a database

**Stage 1 :**

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/89d9415a-2528-489b-94a0-6cf54fbfa15f)

- Users started shopping and added some items the cart. But they are not reflected. So they go back and start from the first.
- Next user went to other instance, this time we lost shopping cart. He thought some bug, So added more items and tried again.
- This time we went to other instance, Where there is no shopping cart. So user stopped using this website. completely and tried another website.

**Stage 2 :**

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/26c789d5-835d-4e46-888f-ab25bd040d44)

- To fix this issue, We can introduce **STICKIMESS OR SESSION AFFINITY in ELB**
- Now user add something in 1st request to shopping cart.
- And second request goes to same instance because of stickiness, And the 3rd request will also goes to the same instance.
- Actually every request will go the same instance. Be'coz of stickiness.
- If EC2 instances goes down, There might issues agian.

**Stage 3 :**
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/551351bf-f7cf-48b5-a9bf-0c0ad727b33f)

- Lets use completely different approach, Use **USER COOKIES**,
- Instead of having EC2 instances store the content of the shopping cart,Let'say that the users is the one storing the shopping cart content.
- So every time it connects to the load balancer. It basically is going to say, by the way in my shopping cart, I have all these things. And that's done though web cookies.
- So now if users talks to the first server, 2nd or 3rd. Each server will know what the shopping cart ccontent is be'coz the user is the one sending the shopping cart  content directly into our EC2 instances.
- So, Now we have acheived statelessness now each EC2 instance doesn't need to know shopping cart contents.

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/baee37d2-5e1a-414a-9f7d-c76101da9d20)

- **BUT NOW HTTP REQUESTS ARE GETTING HEAVIER**
- **Cookies can be altered** ( SECURITY RISK ) 
- **COOKIES MUST BE VALIDATED** (ec2 instances must validate the user cookies)
- **Cookies must be less thatn 4KB**
- **This is the actually a pattern that many web application framework use.**

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/2c320858-993d-480e-b5bc-3f98bb9d5e45)

- Let use conecpt of SERVER SESSION, Now instead of sending web cookies, we just going to send a SESSION ID. And in the background we gonna havemaybe an elastic cage cluster.
- What will happen is that when we send a session ID, we're gonna talk to an EC2 instance. Say we're going to add this thing to the cart.So the EC2 instance will add the car content into Elastic cache.
- And the ID to retrieve this cart content is going to be session ID. So when our user basically does a second request. with a session ID, and it goes to another EC2 instance.
- That other EC2 instance is able using that SESSION ID. To look up the content of the cart from ElastiCache and retrieve that session data.

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/4a5e6187-2c67-43f5-b75c-e73dd6352306)

- Now you want to store the USER DATA, Like profile infor, Address and etc. We are using RDS

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/8683cc6c-91f2-4659-8e93-ad43b553f63b)

- We can use RDS for scaling like using SCALING READS, Read Replicas.

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/9fde8c93-1dbe-4063-8ffc-9d843d20cbec)

 - Lazing loading, User cache looks in the ElastiCache 1st and then if available returns if not it writes into RDS.

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/fb461066-8823-446a-b8d5-b2121e7f605f)

- Now our application is cool, But now we have to SURVIVE FROM DISASTERS as well.


Points to be remebered.
--
- ELB sticky sessions
- Web clients for storing cookies and making our web app stateless
- ElastiCache
- For storing sessions (alternative: DynamoDB)
- Mutaching data from RDS
- RDS
- For storing user data
- Read replicas for scaling reads
- Multi AZ for disaster recovery
- Tight Security with security groups referencing each other

