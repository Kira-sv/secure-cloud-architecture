# Secure Cloud Architecture Plan

## CDN
Static content, such as your HTML and CSS files, is cached by the CDN closer to the users' locations. This lowers latency, increases the web application's overall loading speed, and lessens the amount of direct traffic that reaches your primary infrastructure.

## Load Balancer
Incoming internet requests are divided equally among several application servers by the load balancer. This serves as the application's secure entry point, guarantees high availability, and keeps any one server from crashing under high traffic.

## Application Servers
The Student Management System's core logic is managed by application servers, which also handle users' dynamic requests. These servers should only accept traffic that is routed internally via the load balancer in order to maintain security. This is known as a private subnet. Sensitive student information is safely stored in the database. To guard against

## Database
Sensitive student information is safely stored in the database. The database must be kept completely private and should never be directly accessible from the public Internet in order to guard against potential data breaches and unauthorized external access.

# Public and Private Resources

| Resource | Public or Private? | Explanation |
| :--- | :--- | :--- |
| CDN | Public | Must be accessible to users over the internet to deliver static content globally. |
| Load Balancer | Public | Acts as the entry point for internet traffic, directing it to the private application servers. |
| Application Server | Private | Should only accept internal traffic routed through the load balancer, protecting it from direct internet exposure. |
| Database | Private | Contains sensitive student data and must only be accessible by the internal application servers. |


# Security Controls

## IAM
Only authorized personnel are able to access cloud environments thanks to Identity and Access Management (IAM). These cloud resources should only be managed or altered by authorized administrators and developers.

## MFA
Every administrator and developer account needs to have Multi-Factor Authentication (MFA) enabled. In the event that account passwords are stolen or compromised, this offers an essential second layer of security.

## Firewall / Security Group
Network traffic must be strictly controlled to prevent unauthorized access to backend systems.
* Internet -> Load Balancer = Allowed
* Load Balancer -> Application Server = Allowed
* Application Server -> Database = Allowed
* Internet -> Database = Blocked

## Encryption
To safeguard sensitive personal information, student data must be encrypted both in transit (over the network) and at rest (in the database). This guarantees that information is totally unreadable by attackers even in the event that data is intercepted or storage is compromised.

## Logging
Every system activity, including database queries, infrastructure configuration modifications, and login attempts, needs to be documented. For the purpose of tracking who made particular changes and looking into security incidents, this audit trail is crucial.

## Monitoring
Unusual traffic spikes or repeated unsuccessful logins are examples of suspicious activity that should be closely watched for on the system. Administrators can react to possible threats, such as DDoS attacks, before they result in application outages thanks to early detection.

## Backup
Regular, automated backups of the database must be safely stored. This ensures that in the event of ransomware attacks, hardware failure, or unintentional deletion, student data can be fully restored.

# Principle of Least Privilege

| User | Allowed Access |
| :--- | :--- |
| Administrator | Full access to configure and manage cloud resources, networking, and security groups. |
| Instructor | Read-only access to view all student records through the web application interface. |
| Student | Read-only access to view only their own personal records. |
| Developer | Access to manage application code and servers, with no access to production student data. |


# Shared Responsibility Model

| Responsibility | Cloud Provider or Customer? |
| :--- | :--- |
| Physical data center | Cloud Provider |
| Physical servers | Cloud Provider |
| User accounts | Customer |
| Student data | Customer |
| IAM permissions | Customer |
| Application security | Customer |
| Database access rules | Customer |
| Backups | Customer |

1. *What does Security OF the Cloud mean?*
Cloud security means that the cloud provider is in charge of safeguarding the hardware, software, networking, and physical facilities that power all of the cloud's services. 

2. *What does Security IN the Cloud mean?*
When it comes to cloud security, the client is in charge of protecting their own data, apps, identity management, and operating system settings.

**Part 8: Answer the Architecture Questions**

3. *Which resource should be directly accessible from the Internet?*
The Internet should provide direct access to both the CDN and the load balancer. 

4. *Why should the database remain private?*
Sensitive student information in the database need to be shielded from outside threats. Data breaches and unwanted access are avoided by keeping it private.

5. *Why should users not connect directly to the database?*
The database is exposed to the internet through direct connections, which poses a serious security risk. Only the application server, which serves as a safe intermediary, should be contacted by users.

6. *What is the purpose of a load balancer?*
Incoming user traffic is evenly distributed among several application servers by a load balancer. This guaranties high availability and keeps any one server from failing when under a lot of strain.

7. *What happens if one application server fails?*
After identifying the failure, the load balancer automatically reroutes traffic to the application servers that are still operational [cite: 1]. This maintains the application's uninterrupted online status.

8. *What is the purpose of a CDN?*
To speed up loading times, a CDN caches static files on servers that are closer to the user. By managing the delivery of static content, it also lessens the load on the primary application servers.

9. *Why should administrator accounts use MFA?*
Because they have complete control over the cloud environment, administrator accounts are valuable targets for hackers. Even if a password is stolen, MFA prevents unwanted access by requiring a second form of verification.

10. *Why should administrator access not be given to every employee?*
By adhering to the principle of least privilege, the likelihood of unintentional deletions, incorrect configurations, or breaches in internal security is reduced. Administrative access should only be given to employees who absolutely need it to carry out their jobs.

11. *Why are logging and monitoring important?*
In order to identify suspicious activity and audit access, logging and monitoring offer vital system visibility [cite: 1]. They enable security teams to promptly address threats and troubleshoot performance issues.

12. *Why are backups important?*
Important student data can be promptly restored in an emergency thanks to backups. They guard the system against ransomware attacks, hardware malfunctions, and unintentional data loss.
