Stateful Web App: MyWordPress.com
--
- We are trying to create a fully scalable WordPress website
- We want that website to access and correctly display picture uploads
- Our user data, and the blog content should be stored in a MySQL database.
- Let's see how we can achieve this!

With RDS without READ REPLICAS. MYSQL
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/11e9e28c-1e6c-4ba7-adbe-fa537e89952a)

WITH AURORA MYSQL- READ REPLICAS
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/1a30b6a3-4cbd-4d1e-b666-e1425c36ad6b)

Storing images with EBS
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/d6b4daa7-b131-4da2-a8c2-84b81d907734)

- The problem arrives when we start scaling, So now we have 2 ec2 instances and 2 different AZ. And each of these EC2 instances have their own EBS volumes.
- So what happens is that if i send an image from this instance and stored on that 1st EC2 instance.
- Next time if request goes to 2nd instance and image is not present in that ec2 intances. User gets error.
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/4aa6b392-aa3d-451a-872d-ca0725e2a4c4)
- PROBLEM WITH EBS VOLUMES IS THAT IF WE HAVE ONLY ONE INSTANCE IT IS FINE, BUT WE 2 HAVE SCALING THAT WE WILL GET PROBLEMS.

TO SOLVE ABOVE PROBLEM WE USE EFS (Network filesytem drives)
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/2540ebe8-8d8e-4327-9e4b-ee2143f22fec)

Imp points to remember
--
- Aurora Database to have easy Multi-AZ and Read-Replicas
- Storing data in EBS (single instance application)
- Vs Storing data in EFS (distributed application)
