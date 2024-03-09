Amazon ElastiCache Overview
--
- The same way RDS is to get managed Relational Databases...
- ElastiCache is to get managed Redis or Memcached
- Caches are in-memory databases with really high performance, low
latency
- Helps reduce load off of databases for read intensive workloads
- Helps make your application stateless
- AWS takes care of OS maintenance / patching, optimizations, setup
configuration, monitoring, failure recovery and backups
- Using ElastiCache involves heavy application code changes

Elastic Cache Solution Architeccure - DB Cache
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/f2390aeb-dfa0-48a8-92e8-25cdbcec52b7)

User Session Store 
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/d1421a78-fb17-4a54-9eff-e66bbd4ab3b2)

![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/89e3eaf4-d118-4f5f-865e-0e1facdc1290)

Elastic Cache - Cache Security
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/270890f7-a570-4204-b649-38aa9518fc77)

- ElastiCache supports IAM Authentication for Redis
- IAM policies on ElastiCache are only used for
AWS API-level security
- Redis AUTH
  1. You can set a "password/token" when you create a
Redis cluster
  2. This is an extra level of security for your cache (on top
of security groups)
  3. Support SSL in flight encryption
- Memcached
  1. Supports SASL-based authentication (advanced)

Lazy Loading
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/c7b09631-f39e-442f-8eaa-4018f20e3cdd)

Redis Sorted Sets
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/633cef3a-bddc-4cf3-b721-124dd761069c)
- Real time leaderboard data example like games, shows up 1st 2nd and changes frequently based on scores.
- No need to program in application instaed we can use sorted sets.

List of ports to be familiar with
--
![image](https://github.com/pavankumar0077/aws-sol-architect/assets/40380941/f3f8e2c2-3d31-4948-8289-81e5f6541c02)




