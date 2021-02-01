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
## S3 Storage Classes
- Tiered Storage
  - S3 Standard.
    - All purpose storage class
    - 99.99999999999%(11 nines) durability.
    - Replicates in 3+ Az
    - No minimum object size or retrieval fee.
  - S3 Infrequent Access S3-IA.
    - Objects with real-time access is required by infrequent.
    - 99.9% availability. 
    - 3+Az  replication. 
    - Cheaper than standard.
    - 30 days and 128 KB min charges and object retrieval fee.
  - S3 One zone Infrequent Access.
    - Non critical and/reproducible object.
    - 99.5% availability.
    - Only 1 Az
    - 30 days and 128 KB min charges and object retrieval fee.
    - Cheaper than Standard and standard IA.
  - S3 Intelligent Tiering. (Move objects to different tier based on ML).
    - A storage class available in S3, designed for unpredicted data pattern.
    - Object that aren't accessed for 30 days are moved to the Infrequent tier. Which offers lower cost.
    - If its accessed, it moves to Standard tier.
    - Only monthly automation and monitoring fee is charged
  - S3 Glacier.
    - Long term archival storage (Warm or cold backup).
    - Retrieval could take minutes or hours. (faster the higher the cost).
    - 3+ Az replication. 90 days and 40KB min charge and retrieval.
  - S3 Glacier Deep archive.
    - Retrieval time is 12 hour.
    - Long term archival for cold backup.
    - 180 days and 40KB min
    - Cheaper than Glacier and replacement for Tape storage.
## S3 Lifecycle
  - Can be configured for any versions of object that is not current to be transitioned to a different storage class. 
  - Any older version of object's storage class can be changed.
  - Once moved to a storage tiere from a standard, can't reverse the process to move back to standard storage class using LifeCycle policy.

## S3 Cross region replication.
  - One way replication of data from a source bucket to destination bucket in **different region**.
  - By default, replicated object keep their:
    - Storage class.
    - Object name (Key).
    - Object owner.
    - Object permission.
      - **But this settings can be changed to inherit destination bucket owner or other details**
  - Can be entire bucket, prefix or tags from source bucket to replicate.
  - Replication is not retroactive, meaning only replicates objects that is added after the replication enabled.
  - Replication is only one way.
  - System actions like lifecycle rules are not replicated.
  - Cross region replication SSE-C encryption not supported
  - Only SSE-S3 and if enabled KMS encrypted objects are supported.

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
  - Multipart Upload.
    - Object is broken upto 10,000 parts and uploads in parallel to S3. 
    - Multiple streams of data
    - Enhanced transfer rate.
    - If an individual part fails, only that is retried.
    ```
      # mkfile -n0G 10Gdatafile
      # aws s3 cp ./10Gdatafile s3://my-bucket-name
    ```
    - It is required anything over 5GB but recommended anything beyond 100MB.
## S3 Encryption
  - Encryption is done at object level
  - Encryption
    - At rest.
      - Server side encryption.
         - SSE-S3
          - AES-256 algorithm is used by SSE-S3.
          - S3 manages encryption end to end with less administration over head.
          - S3 data encryption using Keys managed by S3.
          - It uses one of the KMS DEK to encrypt the data, and keys are encrypted and stored with the Objects.
         - SSE-KMS
          - SSE-KMS allows role separation.
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
## S3 Static Website and CORS
- Static Web Hosting
  - Static web hosting will provide a unique endpoint URL that can be accessed by any web browser.
  - Static S3 can host
    - HTML, CSS, JavaScript
    - Media (Audio, movies and images)
    - By default S3 objects are private, the anonymous users has to be enabled.
      - Unblocking public access
      - Make sure the Object permission can be read by un-authenticated user. (From actions make public on all objects)
      - Or create bucket policy to allow any principles to perform S3:GetObject, on resource S3 bucket.
  - S3 logs can be collected for sever access logs.
- [CORS](https://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html)
  - CORS is a security measure allowing a web application running in one domain to reference resources in another.
  - If an application is running a webpage that loads object from a different S3 bucket, CORS can be used.

## S3 Object versioning
- Versioning enabled at per bucket basis.
- Once enabled any operations that would otherwise modify objects generate new version of that original object.
- Once enabled you are billed for all versions of the objects.
- Normally Deleting by adding Delete marker. To permanently delete the objects, select all objects and its versions and delete.
- By deleting the delete marker, you can un-delete an object. 
- MFA delete allows to enforce to use MFA to delete S3 bucket.
- [Delete Object](https://docs.aws.amazon.com/AmazonS3/latest/dev/DeletingObjectVersions.html)
- [MFA Delete](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMFADelete.html)

## S3 presigned URL.
- A presigned URL cab ve created by an identity inside AWS providing access to an object using creator's access permission.
  - By default when a object is accessed, the authorization check is performed at the access of the check. Using the identity of the user.
    - Presigned URLS changes the way object is accessed. 
    - Presigned URL allows to generate a specific URL that has access rights encoded to the URL.
```
 # aws s3 presign s3://bucketname/objectname
```
   - This will generate a preassigned URL with the identity of the user who executed the above command. Now whoever executes the resulting URL will be able to access the object. 
   - The access uses the user identity who generated teh presign URL. 
   - Presigned URL expires in 36 hour.
   - The URL is tied to the person who created. Meaning the User access rights has to be available.
   - If any role which has credential expiry and generates the presigned URL, will have issues after the role credentials are expired.
    - Note: Roles gets temporary credentials from STS and has expiry. 




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

# CloudFront
- CDN is a aglobal cache that stores copies of your data on edge caches.
- Origin
  - The server or service that hosts your content. It can be S3 bucket, web server or Amazon media store.
- Distribution
  - The configuration entity within  CloudFront. Its where you configure all aspects of specific implementation of CloudFront form.
  - Two types
    - Web distribution
      - Speed of content delivery for static files and media files.
    - RTMP
      - Adobe media server protocol for flash
- Edge Location:
  - The local infra that hosts caches of your data. Positioned ion over 150 locations globally over 30 countries.
- Regional Edge Caches
  - Larger versions of edge locations. Less of them but have more capacity and can serve larger areas.

- Origin fetch:
 - If the content is not cached at the edge location, it will perform a origin fetch from origin.
- By default the CloudFront comes up with default domain name at cloudfront distribution. that works with both HTTP and HTTPS.
  - But this can be changed with custom domain name for the distribution, if so need to create SSL certificate proves ownership of the domain. 
  - The cert can be imported from ACM.
- CloudFront is by default public facing, but can be configured to use privately with "Trusted signers".
  - With this configuration in place, only signed URLs or signed cookies needed to access the distribution.

## OAI
- Origin Access Identity. 
  - Usecase: 
    - Only allow access to a resource over CloudFront. And not direct access backend application directly.
    - To avoid lower level of performance by direct access.
    - Dont want customers to directly access object and use OAI.
  - Configured under Origin and Origin group and restrict with the identity created as OAI.
  - The S3 bucket behind the CloudFront will get policy only for Origin access identity. Make sure that if any other statements were in place.

# EFS
- NFSv4
- Designed for Large scale parallel access of data.
- Accessed via mount targets.
- For Linux
- Accessed via VPC, VPN or Direct connect.
- Performance
  - General purpose
  - Max IO
    - Designed for  when a large number of instances need to access the filesystem.
  - Two throughputs modes.
    - Bursting.
      - 100MiB/s base burst.
    - Provisioned
- Lifecycle Management
  - Standard
  - Infrequent access.
- amazon-efs-utils helps to get type of file system efs.
  - `mount -t efs <filesystem id>:/path  /to/system/path`

# Database
## Database models
- DBMS is the database management system.
  - MySQL, MongoDB are example of DBMS. which stores and handles data.
- **SQL (Relational)**
  - Designed to store data with strong built-in relation ship. 
    - Organization storing information about Team members and departments and how they are related.
    - Organize data into tables and link them together based on relation ship.
    - This relation ship help to retrieve and combine data with one or more tables with single query
    - Relational database uses process called normalization.
      - Normalization is a set of data modeling rule, and has two functions.
        - eliminates any redundant data, anything that repeats
        - ensures any data is stored together is depended on each other other wise its separated.
      - Normalization was developed in an attempt to minimize the duplication of data, when storage was costly.
      - Now CPU is most expensive at the moment and also due to scaling issue the movement is towards to non-relational as storage is not any more most costly.
    - In relational database need to create schema in advance, and relation groups the data into tables.
  - Can use Structured Query Language to query the database.
  - If your data has relationship and if its fixed, and not often changed then relational database are faster.
  - Because the relationship is fixed, it struggle with any situation or data which has fluid relation ship.
    - It struggles with social media sites.
    - Hard to scale the relational database, as single system needs to access it all ideally in memory and difficult to separate the data.

- **NOSQL (Non-Relational)**
- [More details](https://database.guide/nosql-database-types/)
  - Are groups of product
    - Key value 
      - DynbamoDB
      - Simple type of db.
      - Its list of keys and corresponding data to values.
      - Excellent method to store data as:
        - excellent way to store data don't have much structures.
        - username and passwords
        - Session states.
        - Used for in memory caching.
      - Able to cope with high velocity of read and write. And can be easily scaled.
    - Document
      - MongoDB, AWS Document DB
      - Used for semi structured data and stored as document.
         - Rather than requiring a schema, it can store data as document in json structure, identified by documnet ID.
         - Example: info about orders, patient record, content management, user profiles, 
    - Column
      - RedShift
      - Data is stored in disk on columns
      - Each record is stored on columns, allows to perform analytic query in efficient way.
      - Analytical, and Datawarehouse products.
    - Graph
      - Neo4j, neptune
      - Designed for dynamic relationship.
      - Social media sites, tracking relationship between different elements.
      - Irrespective of the relational database, no schema to be defined and the relationship changes dynamically.
      - Mostly used by social media sites.

## RDS
- Supports instance types:
  - Burstable
  - Memory optimized
  - General Purpose
- Used to provision fully functional Relational Database Service
- Deployed both single or highly available (Multi) AZ deployment.
- RDS supports 
  - MySQL
  - MariaDB
  - Oracle
  - PostgreSQL
  - MSSQL
  - Aurora - In house developed engine with more features and performance enhancements.
- RDS can move between primary and secondary during failover. The CNAME mapping does changes to backend instance during failover.
- Two types of storage supported
  - General purpose SSD GP2:
    - 3 IOPS per GB
    - Burst to 3000 IOPS
  - Provisioned IOPS SSD (io1)
    - 1000 to 80000 IOPS.
- RDS supports encryption with below conditions:
  - Encryption can be configured when creating DB instances.
  - Encryption can be added by taking snapshot, convert to encrypted snapshot and create DB.
  - Cannot remove encryption.
  - Read replica needs to be at the same state as the primary instance are (with respect to encryption)
  - Encryption snapshots can be copied between region - KMS CMK are region specific.
### RDS backup and restore
- RDS supports manual snapshot-based backups as well as automatic point-in-time recovery-capable backups with a 1-35 day retention period.
- Database snapshot can be performed manually.
- Backups are performed automatically and retention is for 35 days, with once a day with  database backup window.
  - Only the data consumed are billed, and its incremental.
  - Automatic backups are 35 days of max retention is not a long term backup solution.
- Ability to perform point in time recovery.
  - RDS always backup the transaction history in every 5 minutes, allows to perform point in time recovery.
- No matter what method to perform restore, it creates a new Database instance.
  - This leads to reconfigure application during when RDS restore happens.
  - During restore also need to keep special attention to the networking and security group. It will not be as same as original server.
 
### RDS Resiliency: 
[An overview or comparison between Multi Az and Read Replica](https://aws.amazon.com/rds/details/multi-az/)
- Two ways can RDS achieve resiliency.
  - Multi-AZ
    - When provision multi AZ RDS, it creates secondary standby instance,
    - RDS perform `synchronous replication` when Multi-AZ. Copied from Primary node to Secondary Node.
    - Replication happens between instances.
    - RDS perform an Automatic failover during failure.
    - It can happen if there are isolated issues with underlying hardware or configuration upgrade.
      - In the case of software upgrade, it changes the secondary instance first, changes the CNAME mapping then finally update the primary instance.
    - Converting from normal to multi-az occurs downtime.
    - If any RDS but Aurora, CNAME Points to Primary. No additional capability  or control is given for the standby. 
      - From RDS perspective there will be a brief outage during failover. As DNS involved, it might take from single digit sec to double digit. 
    - In RDS other than Aurora its limited to two Availability zone.
    - Backups are taken from Secondary to reduce the impact on Performance.

  - Read replicas
    - Allow systems to scale out to greater amount of read.
    - They are the read only replicas of RDS created on same of different region.
    - It performs `Asynchronous replication`.
    - It is created independently, Meaning CNAME is different.
    - While creating the destination region, network  settings, instance spec, can be chosen.
    - Inorder to create the read replica, the master instance has to have the automatic backup enabled.
    - Can promote a read replica in case of a DR situation.
    - If additional read is needed, or having heavy read application, could point the application to read replicas.
    - 5 read replicas can be attached to a single source.
    - Hierarchy of read replicas are possible. But there will be a lag and application has to support this eventual consistency.
    - Read replicas updates are independent.

### SQL Aurora
- Is a custom designed database engine. 
- Compatible with MySQL and PostgreSQL tools.
- Aurora operates with a radically different architecture as opposed to the other RDS database engines.
  - Aurora uses a base configuration of a "cluster", as shared volume.
  - Max of 64 TiB, 6 replicas and 3 availability zones.
  - A cluster contains a single primary instance and zero or more replicas.
  - Aurora is billed for the storage that is used not the allocation.
  - In the cluster write comes from a single node, and read happens on other two nodes.
- Aurora uses subnet groups, (Which subnet the db has to deploy into)
- Cluster storage:
  - All instances primary and replicas use the same shared storage. The Cluster volumes.
  - Cluster volume is SSD based and can be upto 64 TiB.
  - Replicates data six times across three AZ.
  - Tolerate two failures without writes being impacted and three failures without read impact.
  - Aurora storage is auto healing.
- Cluster scaling and availability.
  - Cluster volume scales automatically and billed for consumed data. Data is backed up to S3.
  - Aurora replicas improve availability, can be promoted to primary instance quickly and allow for efficient read scaling.
  - Reads and writes use the cluster endpoint.
  - reads can use the reader endpoint which balances the connection overall replica instances.
- Instance reservations can be purchased for Aurora instance types.
- It has different types of instances compared to other rds instances.
  - Every cluster creates with a primary instance, and allowed to write to the cluster.
  - It is possible to add additional reader instances within the Aurora cluster.
  - Failover tier
    - Tier0 to tier15 specifies the failover priority. tier0 has higher priority. 
- Aurora is not just an enhancement of RDS, but ut is a new Arch with shared storage, addressable replicas and parallel queries. 
- Different endpoint types
  - Read endpoint 
  - Write endpoints. 
  - Data base instance endpoints. 
- (Backtrack)[https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Managing.Backtrack.html] 
  - Feature allows to rollback the database to the previous state. 
  - Other RDS only allows to restore from the backup.
  - Max is 72 hours.
  - Rolling back with Backtrack will cause downtime. The entire database storage is being rolled back. 
- Any issues happens to one of the writer instance it changes the role (fails over) to next available one. 

####  Parallel Queries and Aurora Global
- Parallel query configured while creating the Database. 
- Its a feature allows queries to be executed on all nodes in the cluster.
  - This is used on larger queries that gives massive benefits. 
- Aurora Global database is selected while creating the database. 
  - It consists one primary AWS region and one readonly secondary region.
  - Aurora replicates data across the region with in secs. Allowing rapid replication with low latency.
  - Useful for global resilience, or need a secondary region serving data.
  - The region info of the cluster will be noted as 'Global'.

#### Aurora Serverless Essentials
- The relation DB without admin overhead. 
- It offers ability to scale the capacity using ACUs(Aurora capacity Units).
- Specify the min and max ACUs
- Proxy fleets
  - A transparent set of proxying instances, without the application knowing the difference.
- Removes complexity of the self managed DB system.
- If the capacity is exceeds, it creates more db instances and adds to cluster. 
- This is selected while creating the DB, choosing Serverless at Database Features.
- Aurora Serverless can be restored from the snapshot.
- It can be treated as just similar as ASG. With no activity the ACUs can be set to zero and significantly reduce the cost. This is called pause state with zero ACUs. 
- But it comes with a cost, as the resume process takes time and until then it takes time. 
- AWS maintains active/warm pool instances for faster scale-up from pause mode.
- It uses private links to add endpoints inside the VPC to connect to the aurora serverless. 
- You cant currently access from a cross VPN or a inter region VPC. 
- To use the query editor it needs to use the Data API.
- Data editor is only available in Aurora Serverless. 

### NoSQL DynamoDB.
- NoSQL DB, features more in dev and sysops exams. 
- Referred to a key value, but not really true its more accurate to describe as a wide column store.
- ITEM, is a collection of attributes upto 400KB inside a table that shares the same key structure as every other item in the table. 
  - Item consists of primary key of the table(partition key or both partition and sort keys).
  - Attributes and values. Example "Name": "customer name"
  - As long of the primary keys (paritition keys or sortkeys) are unique it adds new entry.
  - Items in the table can have various structure in the attribute values.
  - All total of max value of 400KB.
  - When reading or writing the item, have to read the full size of the item.
  - GetItem API is used to get the item, it can be retrieved by partition or Sort keys.
- An attribute can be various available data types Like string, boolean etc. 
- Partition Key
- Sort Key
  - Take an example of DDB table used by different stations to update weather information. IN that case the station ID will be partition Key and the date and time it reports the weather will be the Sort Key. Now if station updates weather in same hour then older hour will not be replaced, as it can be identified with two Sort Keys reported in different time.
- DDB consists of 
  - Tables 
    - Collection of items that share the same partition key or share the same partition key and sort sortkey together with other configuration and performance settings.
    - DDB Tables are created with in the VPC by default. Resource level permissions are not available, but have to be controlled using IAM. 
    - Status code of 200 shows written to DDB. 
    - Default 3 AZ replicas to help failover.  
- An attribute is a Key and Value - An attribute name and value. 
- Every table in a specific region needs to be unique, and a table gets an ARN.

- SCAN and QUERY
  - SCAN can be simply ran on any table that retrieves every single item in the table. 
    - Additional filters can be added during the scan.
    - SCAN operation can consume all capacity as it retrieves full items.
    - Scan helps to search with multiple partition keys.
    - SCAN reads entire table and shows the results.
  - QUERY allow to perform lookups the table without reading every items. 
    - It can retrieve data for single partition key. And has to run against a single partition key while filtering the SortKeys
    - It can filter based on Partition and Sort key. It only consumes the capacity unit for the specific/range of item.
    - Query can be only performed on a single partition key. If you want to work with multiple partition keys have to use SCAN.

- Backup and restore
  - Point in time restore can be enabled at the table level.
  - Manual explicit backup is supported by DDB. Backup contains all the configurations and the indexes.
  - Restoring backup to the new table name.
  - 
- Encryption comes as standard on DDB