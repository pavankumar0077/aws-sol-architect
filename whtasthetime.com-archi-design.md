![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/23fa05f8-cbd3-4e6c-ab6b-404ecb277430)Stateless webapp : Example : whatisthetime.com
==
- Whatls The Time.com allows people to know what time it is
- We don't need a database
- We want to start small and can accept downtime
- We want to fully scale vertically and horizontally, no downtime
- Let's go through the Solutions Architect journey for this app
- Let's see how we can proceed!

1. This is simple start of the application :
  ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/0486c36e-e744-4b3b-a6a7-e4250fac5a32)

2. Eventually the application got popular and getting so many requests. t2.micro can't handle it. We increase the instance type of scaling.
**Scaling Vertically** : Stop the instance and change the type and start the instance.
  - **While upgrading users felt downtime and they are not happy with it.**
    ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/1d6b8724-4c9f-45fc-8ebd-b161ab8af27d)

3. **Scaling Horizontally**
 - Got we got horizontally scale, So we have multple instances, So user will not get downtime and flow is good.
 - **But now instance are increase then remembering the IP of the elastic ip are the tough.**

   ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/3669eb9a-bec4-4629-96f6-c5359d90fa7c)

4. Now we started using Route53 and attached a domain and added all the 3 instances IP addresses, So users and can use it without knowing the ip address. with the domain it self.
   
5. **But if one instance is removed. As we are getting the TTL to 1 hour, So one hour reponses will be gone.**   
  ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b221e0a5-418e-4ca0-afc4-369ea3ec80b5)

6. Now we are using a load balancer to slove the above problem
  ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/41432940-a34c-44bc-9693-dd9c6e15d880)
- Here the problem this adding and removing instance manually is bit time consuming process.

7. Now we will add the instance automatically using Auto scaling group.
   ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/f91e80b8-094d-457f-ae88-bec6b12e1984)
- Here it will automatically scale up and scale down. this is good.

8. But if there is a natural disaster, like earth quake something like that our application will not work. b'coz there in only in one availalblity zone.
- **To solve this problem we have to use Multi-AZ for disastery managment.**
  ![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/45f02fba-2b94-44fa-b560-1ed57436370a)
- This is super cool, we have multi-az DR and all.

9. Now we know that application is well architectured, We need to think about cost as well.
- If we reserve capacity (instance) minimum of 2 AZ will save a lot of cost. If we know it should be running for years.
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/b3790a42-b4b7-41fb-bdb6-950e049a586c)

Things to be remembered
--
- Public vs Private IP and EC2 instances
- Elastic IP vs Route 53 vs Load Balancers
- Route 53 TTL, A records and Alias Records
- Maintaining EC2 instances manually vs Auto Scaling Groups-
- Multi AZ to survive disasters
- ELB Health Checks
- Security Group Rules
- Reservation of capacity for costing savings when possible
- We're considering 5 pillars for a well architected application:
costs, performance, reliability, security, operational excellence
