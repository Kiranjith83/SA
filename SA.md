# Architecture 101 terms:
  ## Cost efficient or Cost effective architecture. 
   - Implement a solution with AWS Product or product features that provides the require service for as little initial and ongoing costs as possible. 
   - Example, hosting large media files effectively storing on storage solutions. 
   - Picking the right tool for right job. 
  
  ## Secure.
   - Secures data and operations from internal and external attack. 
   - Picking right tool for right job, securely. 
   - Choose the product for the security.

  ## Application Session state. 
   - Application session state is the data that rep what customer is doing. What they choosen , what they selected. 
    - example 1: the shopping card selection details chosen by an user.
    - example 2: Preserving the login details when traffic goes to horizontally scalled application server. 
   - Making sure the application state stored in a single server, or saved externally. 
   - If state is saved in the single server or same server, it is called stateless.
   - If the state is saved externally, its called stateful server. This is more preferred as the application servers can be modified without effecting end user state. 

  ## Undifferentiated heavy lifting. 
   - It means any part of application or system that is not specific to the business. 
     - Example: Describes the part of application that is used by every one, and dont have to focus on. AWS takes care of heavy lifting of the infrastructure management while running your EC2 instances.  
   
# Shared responsibility security model.

# Service models.
 - Iaas
 - Paas
 - Saas
 - Faas

# HA and Fault Tolerance.
  - HA:
    - Helps to recover from a failure quickly. 
  
  - Fault Tolerance:
    - Designed to operate throughout a failure with no user impact.

# Disaster recovery
  - RPO 
    - How much a business can tolerate to lose, expressed in time. The maximum time between a failure and the last successful backup. 
  - RTO 
     - The maximum amount of time a system cab be down. How long a solution takes to recover 
  Other consideration.
  - People.
     Are they on call, do they have necessary access and docs to recover. 

# scaling
  - Choice of scaling method (Vertical/Horizontal) determines the cost and how the scaling is configured. 
  - Appropriately selecting the scaling method determines how you architect the application, cost and what if developers need to incorporate to support their application.
  - Elasticiy:
    - capacity to increase or decrease the capacity based on the demand. 

# Tiered Architecture.
  - To be an effective SA, need the understanding of application architecture, then design system architecture for the application. 

# Encryption:
  - Encryption at rest.
    - Symmetric:
      Same key is used to encrypt and decrypt the data. 
      Example:
```
      echo "Cats are Amazing" > hiddenmessage.txt
      gpg -c hiddenmessage.txt
      cat hiddenmessage.txt.gpg
      # Now clear the cached password if you are testing locally.
      echo RELOADAGENT | gpg-connect-agent
      gpg -o output.txt hiddenmessage.txt.gpg
```
  - Assymetric: 
        It is created by multipart key. 
      Example:
```
  # Generate the key
gpg --gen-key
  # Optionally export the public and private keys. And share Public key with the one whom you are sending the data.
gpg --armor --output pubkey.txt --export 'testkey'
gpg --armor --output privkey.asc --export-secret-keys 'testkey'
  # Encrypt the message.
gpg --encrypt --recipient 'testkey' hiddenmessage.txt
  # Decrypt the message.
gpg --output decrypted.txt --decrypt hiddenmessage.txt.gpg 
```
  - Encryption in transit
   - Use of TLS

# AWS WAF (Well architect framework)

  The well architect framework tool is available, based on the pillers.
 - WAF introduces principles for each pillers.
  - Automation to build, modify, and evolve the infrastructure.
  - Allows evolutionary architecture using the data. 
  - [AWS WAF](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc) 

 WAF Pillers and Design principles.
 - Operation Excellence.
    Focus on the ability to use computing resources efficiently to meet system requirements and to maintain that efficiency as demand changes and technologies evolve. 
    - Perform operation as a code.
    - Annotate documentation.
    - Make frequent, small reversible changes.
    - Refine operations procedures frequently.
    - Anticipate failures.
    - Learn from all operation failures.
 - Security.
    Includes the ability to protect information systems, and assets while delivering business value through risk assessments and mitigation strategies. 
    - Implement a strong identity foundation.
    - Enable traceability. 
    - Apply security at all layers.
    - Automate security best practices.
    - Protect data in transit and at rest. 
    - Prepare for security events.
 - Reliability.
    The reliability piller includes the ability of a system to recover from the infra or service disruptions, dynamically acquire computing resources to meet demand and migrate disruptions such as mis configuration or transient network issues.
    - Testing recovery procedures.
    - Automatically recover from failures.
    - Scale horizontally to increase aggregate system availability.
    - Stop guessing capacity.
    - Manage change in automation.
 - Performance efficiency. 
    Includes ability to use computing resources efficiently to meet system requirements and to maintain that efficiency as demand changes and technologies evolve.
    - Democratize advanced technologies.
    - Go global in minutes.
    - Use serverless architecture. 
    - Experiment more often.
    - Mechanical sympathy.
 - Cost optimization. 
    Includes the ability to avoid or eliminate unneeded cost or suboptimal resources. 
    - Adopts a consumption model.
    - Measure overall efficiency. 
    - Stop spending money on data center operations.
    - Analyze and attribute expenditure. 
    - Use managed services to reduce cost of ownership.


# IAM
 - Root account to have MFA to enabled. 
 - Root user is responsible for setting up other IAM users.
 - Creating different AWS Accounts allows to control the blast radius incase something goes wrong with an account.
 ## IAM User
  - One among the identity provided by IAM.
  - 500 IAM users per account.
  - A single user can only be in 10 group.
  - 10 managed policies per user.
  - 1 MFA
  - 2 access keys.
 ## IAM Groups
  - A group of policy.
  - Groups have no credentials. 
 ## IAM Policies
 ## IAM Roles.
  - Roles are never logged into but assumed and gains the permission it carries.
  - With roles, we define the entity who can assume the role at Trust relationships.
  - A role should have trust policy to assume and IAM policy for permissions.
  - While a assume role call is made, 
    - An entity is allowed to assume the role if the IAM trust relationship is allowed.
    - Once its assumed, STS generates a temporary sec credentials with time limit. 
    - Those temp credentials gets the permissions based on the permission policy set on the role.
    - And the identity uses the temporary credentials.
  - Break glass access for emergency access for elevated permissions.
  - Grant AWS Service access.
  - Allows resource from one account to another.
  - Unlike IAM users, IAM roles have short term credentials.
  - sts:AsumeRole can be done by -
    - IAM users
    - AWS Services
    - External accounts.
    - Web identities.

# Billing 
 - Create Billing alarm.

# AWS Organization.
 - A large number of accounts for an organization could be managed by AWS Organization.
 - First account inside AWS Org becomes the master account. 
    - Master account cannot be restricted any way. Master account to be dedicated to just 'being a master account'.
    - This is the root account, and all accounts registered will be part of the organization unit.
 - Generally master account can be used for.
    - IAM users
    - Centralized logging.
    - Consolidated billing. 
 - Service Control Policy: 
    - Defines what a service account can do. 
    - It can be applied to individual account, or Organizational Unit and policy applies recursively. 
 - AWS accounts to consolidate bill. 
    - Individual accounts bills are consolidated to master account. 
    - Member account passes the billing to the master account. 
 - Restrict access. 

### Switch roles between accounts.
 - Is a method of accessing one account from other using only one set of credentials. 
 - You will have a master AWS account, which has one or two role with appropriate permission. 
  - Now the roles on master account are allowed to assume roles in organization unit accounts.
 Steps:
   - Login as IAM user on master account. 
   - From the console, use switch the Role option. 
    - AWS Organization creates an IAM role automatically on the accounts to switch into, called "OrganizationAccountAccessRole"
   - If you invite an account, make sure to have the Roles that can be switched is created. AWS Organization will not create if an account is added by invite.      

# S3
  - Read and write consistency with new file
  - Eventual consistency with update, delete of existing it.
  - 99.99% Availability 
  - 99.99999999999% Durabilities
  - Tiered Storage
    - S3 Standard.
    - S3 Infrequent Access.
    - S3 One zone Infrequent Access.
    - S3 Intelligent Tiering. (Move objects to different tier based on ML)
    - S3 Glacier.
    - S3 Glacier Deep archive.
      - Retrieval time is 12 hour.
  - Lifecycle Management (Moves to different Tier of storage).
  - Versioning
  - MFA for Delete. 
  - Secure using ACL and Bucket policy.
  - Charge:
    - Based on storage
    - Based on number of requests.
    - Charged on Storage management.
    - Data transfer pricing.
    - Transfer acceleration.
    - Cross region replication.
  - 0 to 5 TB file size and Unlimited storage. 
## S3 Permission
  - Comes with legacy sec baggage.
  - Very S3 bucket is owned by the account.
  - Only entity initially has access is the account that created the bucket.
  - Identity Policies and attach to IAM Entities.
    - You cannot provide S3 identity policy for IAM Identities that you have no control. (Or from other IAM Account).
  - What if if you want to apply various access to identity that you dont control?
    - Use Resource policy.
      - Resource policy with S3 bucket is called bucket policy. 
      - Can be used to apply any identities accessing the bucket.
      - It doesn't matter which account holds the identity. 
      - You attach S3 bucket policies at the bucket level (i.e. you can’t attach a bucket policy to an S3 object), but the permissions specified in the bucket policy apply to all the objects in the bucket.
      - Any policy that has explicit denies will override any allow.
    - ACL, or access control list.
      - Legacy method, and suggests to use Resource policies.
      - They control access in simple way for Bucket and objects.
  - Block public access, is a setting applied on top of any existing settings as a protection.
    - Block public access overrules any other public grant.
  >
    - If you’re more interested in `“What can this user do in AWS?”` then IAM policies are probably the way to go. You can easily answer this by looking up an IAM user and then examining their IAM policies to see what rights they have.
    - If you’re more interested in `“Who can access this S3 bucket?”` then S3 bucket policies will likely suit you better. You can easily answer this by looking up a bucket and examining the bucket policy.

### When to use IAM policies vs. S3 policies
  - [MUST READ HERE](https://aws.amazon.com/blogs/security/iam-policies-and-bucket-policies-and-acls-oh-my-controlling-access-to-s3-resources/)

## S3 Upload.
  - Single PUT upload.
    - Limit to 5GGB in size.
    - Runs into performance issue, if the size is higher, as it uses single steam of data.
    - As its single stream, it will not get the maximum bandwidth.
    - If did fail, the entire operation has to re-run.
  - Multipar Upload.
    - Object is broken upto 10,000 parts and uploads in parallel to S3. 
    - Multiple streams of data
    - Enhanced transfer rate.
    - If an indiidual part fails, only that is retried.
    ```
      # mkfile -n0G 10Gdatafile
      # aws s3 cp ./10Gdatafile s3://my-bucket-name
    ```
    - It is required anything over 5GB but recommended anything beyond 100MB.
## S3 Encryption
  - Encryption
    - At rest.
      - Server side encryption.
         - SSE-S3
          - AES-256 algorithm is used by SSE-S3.
          - S# manages encryption end to end with less administration over head.
          - S3 data encryption using Keys managed by S3.
          - It uses one of the KMS DEK to encrypt the data, and keys are encrypted and stored with the Objects.
         - SSE-KMS
          - SSE-KMS allows role seperation.
          - Unlike in SSE-S3, the user who has access to object can decrypt the data.
          - A specific KMS master key is used to encrypt the data.
          - Ideally customer can create a Customer Managed Keys.
          - And the permission specifically can be defined at the CMK.
          - This enabled  to have specific IAM user/role who has permission to the KMS key to decrypt the data.
          - S3 Admin and KMS key access can be given to two different users for role separation.
         - SSE-C
          - Server side encryption with customer managed key.
          - When uploading object, you also provide the encryption key and heavy load of encryption is managed by S3.
          - Once the encryption is done, key is discarded. 
          - Admin heavy process in managing the keys. Customer should take care of key management.
      - Client side encryption.
        - Encrypt and upload to S3.
        - Use client, application or manually perform the action.
        - Example: Backup application uses S3 storage, backup data is encrypted prior to upload to S3.
    - At transit

# Serverless

## APIs and MicroServices.
  - A small component of a service which is self contained and can operate itself.
  - APIs allows to access a microservice.
  - Event Driven Architectures.
    - The one which operates during an event. 
    - Example: File being uploaded and take an action.
    - Opposite to constant polling system, which need more resources to get an event. 

  - Serverless
    - It has two components.
      - Function as a service.
        - A service model to utilize short running or temporary compute. The code execution based on event, or at a scheduled time.
      - Backend as a service.
        - Like ID providers, cognito.
        - A service model prioritize the consumption of third-party providers, remove lot of the dependencies. Example, Data base provider, ID provider.

## Lambda:
  - Function as a service.
  - Executes upto 15 minutes.
  - Invoked by events, time, or by a different service.

Example:
  - [Git Link:](https://github.com/linuxacademy/content-aws-csa2019/tree/master/lesson_files/03_compute/Topic4_Serverless/lambda)
  - Below sample function creates thumbnails whenever an image is uploaded to a S3 bucket (dst_bucket). 
  - Configure Lambda using below commands.
```
mkdir /tmp/lambdafunction
cp lambda_handler.py /tmp/lambdafunction
cd /tmp/lambdafunction
wget https://files.pythonhosted.org/packages/ae/2a/0a0ab2833e5270664fb5fae590717f867ac6319b124160c09f1d3291de28/Pillow-5.4.1-cp37-cp37m-manylinux1_x86_64.whl
unzip Pillow-5.4.1-cp37-cp37m-manylinux1_x86_64.whl
rm -rf Pillow-5.4.1.dist-info
zip -r9 lambda.zip PIL lambda_handler.py
```
  - The event is driven from the upload S3 bucket trigger, where the images are uploaded.
    - Configure the S3 bucket events to notify Lambda from the s3 upload bucket.

## API Gateway
Two types of APIs:
  - Rest API:
    -  Is simpler and wider compatibility. 
    -  Uses requests and response style exchange and its stateless.
    -  Every time a request is made its considered as Brand new communication
  - WebSocket 
    - The transaction that needs higher through put, webSockets has Better performance.
    - A connection architecture is used, and communicate in a constant fashion. 
    - A push will happen to large consumers at once.

Overall steps in creating the API Gateway.
  - Create API -> Create resource -> Use a method on how to interact with the resource -> Finally choose the integration method
    - [Sample](https://github.com/linuxacademy/content-aws-csa2019/tree/master/lesson_files/03_compute/Topic4_Serverless/apigateway)
    - [AWS Documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/integrating-api-with-aws-services-lambda.html)
  - Finally create the stage to publish the API.
  
  - Enabling API cache for returning similar requests.

## Step functions.
  - Addresses the short runtime of Lambda, Stateless of Lambda
  - Provides State machines. 
  - Can orchestrate other AWS services and maintain the state.
  - State machines can be operating for one year.
  - Allows multiple Lambda to be coordinated. 
  - Example: 
    - User approval cycle for a change management. 
    - [Example use case:](https://github.com/linuxacademy/content-aws-csa2019/tree/master/lesson_files/03_compute/Topic4_Serverless/StepFunctions)

# Container-Based Compute and Microservices

## Docker
  - Virtual Machines are created by taking physical machine and carving out resources dedicated to the VMs. 
  - With the containers it creates isolated process on top a physical or virtual server. 
    - Shares the underlying operating system but isolated process. Containers are isolated from other containers.
  - VMs are like individual houses. 
  - Containers are like an apartment.
  - Choosing between containers and VM there is no once choice that fits all.
    - Mostly based on choice between Monolythic or Microservice.
  
  - Running docker:
```
sudo amazon-linux-extras install docker
sudo service docker start
sudo usermod -a -G docker ec2-user
```
  - Build a sample app image and push to repo.
  - A docker image is a file system, that containers number of Layers. A Docker image consists of several layers. Each layer corresponds to certain instructions in your Dockerfile. The following instructions create a layer: RUN, COPY, ADD. The other instructions will create intermediate layers and do not influence the size of your image. 
  
```
sudo yum install git
git clone https://github.com/linuxacademy/content-aws-csa2019.git

cd content-aws-csa2019/lesson_files/03_compute/Topic5_Containers/Docker/
docker build -t containercat .
docker images --filter reference=containercat
docker run -t -i -p 80:80 containercat

docker login --username YOUR_USER
docker images
docker tag IMAGEID YOUR_USER/containercat
docker push YOUR_USER/containercat
```

# Networking Fundamentals

## OSI Model.
  Each layer adds benefits of layer below that.
  - 7 Application
    - Web browser, HTTP
    - Application sees communication between two Layer 7. But it uses all the lower layers.
  - 6 Presentation
    - TLS adds Encryption.
    - All about conversion, compression and encryption of data.
    - FTP, SSH are added.
  - 5 Session
    - Session are introduced.
    - The initiated and responded traffic will be part of the same traffic. Example IPtables stateful firewalls.
  - 4 Transport
    - Reliability
    - TCP/UDP protocol works here.
    - Uses `Segments`: For ordering and error correction.
    - Making sure the packets segment is received in order it has send and checks error.
    - Adds the concept of Ports.
  - 3 Network 
    - End to end communication.
    - `Encapsulates packets` to IP address.
    - Adds capability to cross to different network (Router).
    - Each device has its own unique IP address.
    - The packets has Src and Dst IP.
    - Single connection or single channel communication.
  - 2 Data link
    - Base level networking
    - Uses Layer 1 and adds capability.
    - Adds Mac address, used to identify individual equipment.
    - Uses `Frames`: A piece of data with Src and Dst Mac address.
    - Communicates over local network (Network HUB).
    - Adds control on who can talk to whom.
  - 1 Physical
    - Base level networking
    - Reception or Transmission of Data.
    - Radio freq spectrum.
    - Describes electrical, optical, mechanical medium.
    - No individual device in Layer 1, It is a shared medium. 

## IP addressing
Traditional way of sharing IPs to Small/Medium or large Org, with private IP range on each class.
  - Class A /8
  - Class B /16
  - Class C /24
  
CIDR:
 - In addition to Classes, CIDR helps a better way for allocating wider range of subnets.
 - 10.0.0.0/16

## Subnetting.
[Online Calculator:](https://subnettingpractice.com/calc.html)
[Online calculation cheetsheet:](https://www.pcwdld.com/subnet-mask-cheat-sheet-guide)
> Current Network:
10.0.0.0/16  -> Split the CIDR 

10.0 > Network  0.0 -> Host range 

> Split to two individual network by incrementing prefix 16

The 1 bit we borrowed is represented in "" ' "". Remember that this is binary, meaning that this borrowed bit can either be 0 or 1. In effect, by borrowing one bit, we can create 2 subnets:

10.0.0.0/16 
Current Subnet 
```
00001010    00000000    00000000    00000000
```
Now to break this into two halfs ()
```
00001010    00000000    0'0000000    00000000
00001010    00000000    1'0000000    00000000
```
10.0.0.0/17
How 17?  -> The total number of CIDRs. 
What are the Networks 

10.0.0.0/17 
10.0.128.0/17 
How 0 and 128 ? As we divided into two halfs then we did 256/2 = 128. SO zero and 128 two equal parts. 


Now to break this into more.
```
00001010    00000000    00'000000    00000000
00001010    00000000    10'000000    00000000
00001010    00000000    01'000000    00000000
00001010    00000000    11'000000    00000000
```
Now this is 4 subnets. 
10.0.0.0/18 
  We could create 4 parts with 0 and 1 combinatiopns. 
  256/4 = 64 . 
  The iprange becomes 
 10.0.0.0/18
 10.0.64.0/18
 10.0.128.0/18
 10.0.192.0/18

or use  ipcalc -b 10.0.0.0/18

 Now to break this into even more.
```
00001010    00000000    000'00000    00000000
00001010    00000000    010'00000    00000000
00001010    00000000    001'00000    00000000
00001010    00000000    100'00000    00000000
00001010    00000000    110'00000    00000000
00001010    00000000    011'00000    00000000
00001010    00000000    111'00000    00000000
```
10.0.0.0/19
ipcalc -b 10.0.0.0/18 shows first Broadcast
```
[me@my-host ~]⎈ : ipcalc -b 10.0.0.0/19
BROADCAST=10.0.31.255
[me@my-host ~]⎈ : ipcalc -b 10.0.32.0/19
BROADCAST=10.0.63.255
[me@my-host ~]⎈ : ipcalc -b 10.0.64.0/19
BROADCAST=10.0.95.255
[me@my-host ~]⎈ : ipcalc -b 10.0.96.0/19
BROADCAST=10.0.127.255
[me@my-host ~]⎈ : ipcalc -b 10.0.128.0/19
BROADCAST=10.0.159.255
[me@my-host ~]⎈ : ipcalc -b 10.0.160.0/19
BROADCAST=10.0.191.255
[me@my-host ~]⎈ : ipcalc -b 10.0.192.0/19
BROADCAST=10.0.223.255
[me@my-host ~]⎈ : ipcalc -b 10.0.224.0/19
BROADCAST=10.0.255.255
```
> A trick, increment the CIDR for more network. 
In the case of 10.0.0.0/16 network, subnetting will have below network.
  - /17 will have 2 network.
  - /18 will have 2 network.
  - /19 will have 4 network.
  - /20 will have 16 network.
  - /21 will have 32 network.
  - /22 will have 64 network.
  - /23 will have 128 network.
  - /24 will have 256 network.

## IP routing.
 - BGP Protocol. - Advertise and automatically learns the Routing.

## Firewall.
 - Layer 3 (Network) - Source/Destination IP addresses or Ranges
 - Layer 4 (Transport) - Protocol and port num,ber
 - Layer 5 (Session) - as Layer 4 but understand the session.
 - Layer 7 (Application) - Application specifics eg, HTML path, images

## Egress only Internet Gateway.
  - Egress only internet gateways provide IPV6 instances with outgoing access to the public internet using IPV6 but prevents the instances from being accessed from the internet.
  - NAT isn't required for IPV6, and so NAT GWs aren't compatible with IPV6.
  - Egress only gateways provide the outgoing only access of a NAT GW but do so without adjusting any IP settings.

# DNS Route 53
 - DNS root zone top level database contains top level domain (TLD), managed by large organization. 
  - .com is deligated to veriSign global registery services. 
  - Inside the top domain, has the subdomains. 
 - Zone files represents the area of the DNS global database. 
 - Records are type of records saved on Zones.
 - Authoritative: The one who has the authoritative for a zone. 
  - When a root domain deligates the top level domain name .com to veriSign, they allow verisign to give them Name Server. 
  - Now veriSign becomes the authoritative for .com.
  - A authoritative response is from the server who is authorized to serve the Zone.
  - For example, once you register the domain 'mydomain.com', the veriSign deligates a NameServer for mydomain.com and it becomes authoritative. 
 - Flow:
  - Local system ask for domain.com -> Root server for .com. -> Ask .com. authoritative server who is domain.com -> gets Name server for (Authoritative server) domain.com -> DNS resolver contacts NS of domain.com and gets authoritative answer.
  - dig +trace 'domain.com'

## Route 53
  - Private hosted zone.
    - Need enableDNSHostnames and enableDnsSupport at VPC.
    - Split view DNS is supported, giving Public and Private queries different records for same query. It is setup with same record with different targets.
      - How it works? 
      - If any zone has same record, inside the VPC the private zone overrides the public zone.
  - Public hosted zone.
  - Record types:
    - A IPV4
    - AAAA IPV6
    - CNAME for alias
    - MX
    - NS - used to delegate authority for a domain server.
    - TXT - used to descriptive text in a domain, used to verify the domain ownership.
    - Alias record, extension of CNAME but can be used like A record.
  - Health Checks
    - Health checks that monitor the health of an endpoint
    - It can perform below health checks.
      - Monitor the Endpoints.
      - Status of other health checks (calculated health check)
      - State of CW Alarms.
    - Global health check system that checks an endpoint in an agreed way with an agreed frequency.
      - If >18% of checks report healthy = healthy
      - <18% healthy = unhealthy 
    - Types of Health Checks
      - HTTP and HTTPS connection check in less that 4 seconds.
      - TCP health check: tcp connection within 10 seconds
    - The health checks status can be also Inverted and used.
  - [Routing Polcy:](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html)
    - Simple:
      A simple routing policy is a single record within a hosted zone that contains one or more values. When queried, a simple routing policy record returns all the values in randomized order. 
      - Pros: Simple, the default, even spread of requests
      - Cons: No performance control, no granular health checks, no influence on which IP is returned or not to be used as LoadBalancer. If Alias is picked, we can only select a single Alias record.
    - Failover:
      Enhances the ability to failover from one to another record based on health check.
      - Failover routing allows you to create two records with the same name.
      - One is designated as the primary and another as secondary. Queries will rewove to the primary, - unless its unhealthy in which case route 53 will respond the secondary.
      - Failover can be combined with other ty;es to allow multiple primary and secondary records. Generally, failover is used to provide emergency resources during failures.
    - Weighted routing:
      Control amount of traffic reaching specific resources.
      - Route traffic to specific resource based on the weight. 
      - The higher weight number, the more traffic it gets.
        - Create 3 SSIDs with 3 different weights. 
          - with weight 1
          - with weight 2 
          - with weight 7 
            - Traffic will be destributed amount 10%, 20% and 70% respectively.
      - SetID unique string, unique among the group of the record.
      - Used for testing new features, and small portion of DNS to be redirected to certain resources.
    - Latency:
      With latency based routing, route53 consults a latency database each time a request occurs to a given latency based host in DNS from a resolver server. Record set with the same name are considered part pf the same latency based set. Each is allocated to a region. The record set returned is the one with the lowest latency to the resolver server.
      - It maintains a database of latency between internet based endpoints. 
      - The record is returned on the region based record which is configured at the Latency routing policy.
      - Lookup will resolve or return the one near to the client.
      - It is not only based on Geography, but also based on the ISP.
    - Geolocation:
      Lets one choose the resources that serve traffic based on geographic region from which queries originated. 
      - With Geolocation pick a location Country, continent, and SetID.
      - A crucial difference between Latency and Geolocation is that, unless there is a geolocation based on region configured it will return no record for the client.
      - Can be used to limit the region based lookup. 
      - When a given resolver attempts a lookup, it returns only record with matching name and matching incoming location.
      - Different location of granularity can be applied to the location (Countries, Continents etc).
      - Default can be used to choose to return traffic for any geo location.
      - Order of traffic returned is based on the Geoproximilty.
    - Multivalue Answer:
      - Same like simple routing policy but allows multiple records with the same name. 
      - Returns upto 8 of the records in random.

