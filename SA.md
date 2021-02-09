# Certified Solution Architect Notes
***Disclaimer: Below information may or may not be correct. This is solely created for my own reference. You are welcome to refer on a condition that the author is not responsible for any issues related to below content.***
Topic to be learned to pass
## Core Services
- Compute
- Security, Identity and Compliance
- Network and Content Delivery
- Storage 
- Databases
## Other Services
- Analytics
- Desktop & App Streaming
- Management and Governance.
- Machine Learning
- Migration and Transfer 

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
 - Centralized access, Shared access, Granular Permissions, Identity Federation (AD, using any IDP).
 - Provides temporary access (Application allowing to upload files to S3).
 ## IAM User
  - One among the identity provided by IAM.
  - 500 IAM users per account.
  - A single user can only be in 10 group.
  - 10 managed policies per user.
  - 1 MFA
  - 2 access keys.
 ### IAM Root account
 - God Mode user
 - As a best practice enable MFA.
 ## IAM Groups
  - A group of policy.
  - Groups have no credentials. 
 ## IAM Policies
  - Json formatted documents gives permission as to what a user can do.
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
#### Partition Key
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
#### SCAN and QUERY
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
- Encryption comes as standard on DDB
- By default the tables are created on region base.
  - Global table functionality can be enabled on the tables by enabling Streams then add list of regions to the tables to replicate to.
  - Global tables can be only enabled on an empty table.
- DDB comes with full integration to Cloudwatch.
- When to use DDB over other DBs.
  - Suites unstructured data, like keys and values, Json data and more complex data. 
  - DDB is data base as a service product. It is serverless from customer perspective. 
  - If its not a fixed schema, if its web scale app, ID federation, any lightweight DB all key words goes in direction of DDB.
#### Performance and Billing 
- DDB has two read/write 
- Partitions are the low level entity which stores the data. 
- DDB achieves the high level of performance by splitting the data to the partitions. 
  - DDB hashes the partition key and denotes where the data is stored on the partition.
- DDB increase the number of partitions when the demand is increased. 
- The read and write capacity is distributed across each partition tables. 
- Reading and Writing performance is depending on the partition performance. 
- A partition is replicated into 3 AZs. The partitions are residing on Nodes.
  - Leader node makes sure data is replicated to the other nodes, and leader nodes guarantees access to the recent updated node.
  - Eventual consistence occurs if the data is read from Non Leader node, immediately after commiting the data.
  - By default the read is eventual consistent read, which is half of the cost of strong consistent (read from leader).
  - Read capacity Units:
    - One RCU is 4 KB of data read from a table per sec in a strongly consistent way. 
    - Reading 2 KB of data consumes 1 RCU. Reading 4.5 KB of data takes 2 RCU. Reading 10x400 bytes takes 10 RCU.
    - If eventual consistent reads are okay, 1 RCU can allow for 2x4KB of data reads per sec. 
  - Write Capacity Untis.
    - One WCU is 1 KB of data or less written to a table. An operation that writes 200 bytes consumes 1 WCU, an operation that writes 2 KB consumes 2 WCU. 
    - Five operations of 200 bytes consumes 5 WCU.
    - Example 1:
      - A system needs to store 60 patient records of 1.5 KB each and every min. What ECU should be allocated on patient record table? 
        - 60 records per min =~ 1 per second (and the DDB RCU/WCU buffer can smooth this out if not)
        - Each record is 1.5 KB. 1 WCU = 1 KB per sec, so each record requires 2 WCU.
        - WCU is per sec, so setting of WCU should be 2. 
    - Example 2:
      - A weather application reads data from a DDB table. Each item in the table is 7 KB in size. How many RCUs should be set on the table to allow for 10 reads per sec?
        - 1 item is 7 KB. So need 2 RCU per item in a sec. (1 RCU is 4 KB)
        - 10 reads per sec for 7 KB = 10x2 = 20 RCU
        - The above applies for Strong consistency. 
        - The default is eventual consistency, which allows 2 reads of 4KB with 1 RCU. 
        - So half of strong consistency is needed which is 10 RCU.
-  Read/write capacity modes. 
  - Provisioned.
    -  Predictable workload by calculating the RCUs and WCUs for the application workload.
  - On-demand. 
    - Used for application workload which is too complex to predict, system determines the WCUs and RCUs. 

#### DynamoDB Streams and Triggers
- DDB streams are enabled on per table.
- Stream provides an ordered list of changes that occur to the items within a DDB. A stream is a rolling 24 hour window of changes.
- All stream has ARN.
- Stream can triggered with Lambda, invoking function whenever items are changed in DDB.
- Types of stream -
  - KEYS_ONLY
    - Whenever an item is added, updated or deleted the keys of the items are added to the stream.
  - NEW_IMAGE
    - The entire item is added to the stream "post-change"
  - OLD_IMAGE
    - The entire item is added to the stream "pre-change"
  - NEW_AND_OLD_IMAGES
    - Both the new and old version of the item are added to the stream.
- An event driven function can be triggered with the stream trigger.
  - For example, having KEYS_ONLY and trigger the lambda as soon as a new item is added.

#### DynamoDB Indexes
- What if we want to retrieve information for different partition keys? 
 - Scans could get the data but it will read all items in the table, and it consumes the capacity of whole capacity allotted. 
- It provides an alternative representation of data in a table. Which is useful for applications with varying query demands. 
- Any access patterns which doesn't fall into the table - Index can be used. 
- Two types. 
  - Local secondary Indexes.
    - It has to be created at the time of table creation.
    - They use the same partition key but an alternative sort key.
    - They share teh RCU and WCU values of the main table.
    - Allows to perform query on the Index, at Sort Keys created instead of item partition key.
    - It is kind of creating new item with different Sort Key, which has the same data.
    - Limited to 5 indexes.
  - Global Secondary indexes.
    - It can be created at any point after the table is created.
    - They can use different partition and sort keys. 
    - They have their own RCU and WCUs.
    - 20 GSUs limit per table are soft limit.
    - GSU dont share the data with the table. 
    - Only eventually consistent queries to be performed and strongly consistent will not be available. 
    - Projected attributes can be set on GSUs as they can be used to fine tune the attributes that is really read by "application", to improve the performance. 
      - Access to non projected attributes will have a large performance issue as well (Full table needs to be read.).

#### In-Memory Caching DAX
- DAX is dynamoDB in memory accelerator. 
  - If data is needed within micro sec, DAX can be beneficial. 
  - DAX runs inside the VPC uses cluster arch With one or more node. 
  - When the item is read once, it resides in DAX, a process called cache HIT.
  - Kind of proxy, which leaves on same computer instances.
  - DAX is designed for high index read application that can't afford read latency.
  - Application require strongly consistent ones are not recommended, only good for eventual consistent reads. 

## Elastic Cache.
- Historically, EC was used in DynamoDB, but later AWS delveoped DAX.
- ES supports Redis and MemecacheD .
- It is in-memory data store and two common use cases are:
  - Offloading database reads by caching responses, improving application speed and reduce costs.
  - Storing user session state, allowing for stateless compute instances(used for fault tolerance architectures).
- It is generally used with Key Value databases.
- But also used to store simple session data.
- It can also use with SQL database engines.
- A performance enhancing, and to be part of fault tolerance arch for stateless application.

# Load Balancing
- Historically, LBs were only able to route traffic to instances inside an AZ, causing uneven traffic distribution if AZ instances are not equal. 
  - To resolve this disparity introduced the cross zone loadbalancing, which is enabled by default now.
## CLB
- Supports layer 3 and 4 (TCP and SSL) and some HTTPS features(Configuring HTTP health check)
- Its not a Layer 7 device so no real HTTPS. 
- One SSL Cert per CLB, which can get expensive for complex deployments. 
- SSL Offload, can be connected to AutoScaling Group.
- Health check min time is 5 sec.
## ALB
- Operates at L7 OSI model
- ALBS are recomended as the default LB for VPCs. Better performance and cheaper than CLB. 
- Content rules Host-based and Path based rules can be set for routing traffic.
- ALB Supports EC2, ECS, EKS, Lambda, HTTPS, HTTP/2 and WebSockets and can integrate with AWS WAF.
- Better support with COntainers and Microservices. 
- Traffic is routed as Targets -> Target group -> Content Rules.
  - Target is something that can point the connection at. The target types can be EC2 instances, Lambda Functions, IP address.
  - Target groups are collection of targets.
- ALB supports multiple SSL certificates using SNI.
- ALB can have a custom port for heath check (Override/Traffic port feature)
- ALB default rule gets added whenever a rule is not configured. 
- Target group target status - unused means the target group is not registered to any ALB.
- ALB Rules can be based on below attributes:
  - Host header
  - path
  - http header
  - http request method
  - query string
  - source IP
## NLB 
- Operates at Layer 4.
- Less latency because no processing above Layer 4 is required, with highest performance. 
- Static IP address 
- source IP preservation.
- Target can be IP address.

# Auto Scaling
- ASG defines how the Launch config/template to be scaled in/out.
- Min and Max number never exceeds and desired capacity is modified based on metrics.
- Scaling policies and scheduled actions allows to automatically scale in/out.
- Scaling policies
  - Simple scaling policies based on instance metrics. Example scale up based on CPU metrics.
    - Example, CPU utilization is 50% then add 1 instance.
    - It will not add another instance until the wait time is elapsed. 
  - Target scaling policy
    - We can define an ideal value and make sure the ASG keeps the metrics around the same.
    - Say if the avg CPU value is set to 60%, if it goes above the value, it will add instances and goes below removes the instances.
  - Stepped policy
    - If CPU is 20 % to 50% add 1 instance. 
    - If CPU is around 90%, then add 10 or more instance. 
    - This is used in a different scenario as Simple scaling policy will only scale linearly and wait for timeout. But Stepped scaling policies are useful in different level of scaling. 
- An ALB association can be done from ASG, by selecting the Target Group. This allows instances to be automatically registered to the target group. 
  - The target group has to be associated with the ALB. 
- Health check type can be ELB/EC2 at ASG.

## Launch Config
- What has to be launched. 
- Initial way of creating ASG.
- Cannot change a Launch config, but can copy to new.
  - This is to avoid any impact to any Existing ASGs using the Launch config. 
## Launch Templates
- Preferred
- Addresses some of the weakness of legacy launch configurations
  - Versioning and inheritance.
  - Tagging
  - More adv purchase options.
  - New instance features:
    - Elastic graphics
    - T2/T3 unlimited settings
    - Placement groups
    - Capacity reservations
    - Tenancy options.
- A launch template is immutable but can create new version using versioning.
  - Versioning gives ability to pick, a default, latest or specific version at ASG while launching or scaling.
- Launch template can be used to directly launch EC2 instances, by standardizing the config.

# VPN 
- Components
  - Customer gateway:
    - Represents a physical piece of hardware at customer end.
    - Its generally a router or hardware at the customer end. 
    - Capable of IPSec VPN connectivity using Static or Dynamic routing.
    - Customer GW with AWS COnsole is the logical representation.
    - Configure:
      - Create the CGW using Static or Dynamic Routing is used at the hardware. 
      - Static routing - Share the VPC and home network address to each end.
      - Dynamic routing - Network details are shared automatically over BGP. For that just share the Autonomous System Number (ASN) of customer GW.
  - VPG Virtual Private Gateway.
    - It is a GW like IGW, or NAT Gateway, and VPC router routes the traffic to VPGW.
    - VPGW can be attached to a Single VPC and it acts as a endpoint for the VPN Tunnels.
  - VPN Connections:
    - Site to Site VPN Connections.
      - THIS IS THE LOGICAL ENTITY THAT LINKS THE VPW AND CGW
      - Different types of configuration connections can be done. 
        - Single Tunnel to Single customer gateway. 
        - Two tunnels to Single customer gateway.
          - Tunnels are multiple AZs connecting to single Customer Gateway.
        - VPN Connections between two different customer gateways and VPN connection has two tunnels going to Customer Gateways.
          - Support fully high availability.
      - Once the VPC configuration is done download the configuration.  
- VPN Connection is quick to setup in minutes
- Per hour cost.
- Data charges for outgoing, heigher than Direct connect. 
- VPNS economical if lower data req. 
- VPNs performance depend on CGW devices. 
- VPNs use encryption end to end, perfromance impacted with the CPU of CGW. 
- Variable performance due to internet latency. 
- Cheaper and quick to setup.
- Route propogation preference as below:
  - Routing in general, local route takes priority.
  - In route table with longest prefix is preferred
  - If same route mentioned twice then the static route is preferred. 
  - Any Direct is prefered over VPN.
  - Dynamic propogated leadned from BGP got lowest pref.
## When and where to choose VPN 
- Urgent need 
- Cost constrains needed cheap and economical
- Low end or consumer hardware 
- Need Encryption
- Flexibility to change locations
- High availability.
- Short term connectivity. 
- As a cheaper alternative for DX
- As an additional layer of HA for DX.
# Direct connect DX
- When you need speed and consistency. 
- 1Gbps or 10Gbps dedicated line.
- It uses customer or partner router to get connected physically.
- Runs over cabling done from Customer end via DX location to AWS Direct connect.
- Low and consistency latency with fast speed.
- As its physical, it takes a number of days before it gets active.
- It might take months if the cabling needs to be done DX location to customer office.
- Private VIF and Public VIF
  - Private VIF created to access to single VPC.
  - Public VIF created to access to Public AWS Services endpoints.
- The connection is not encrypted. 
- Direct connect is a one piece of physical cable and it is not highly available. 
  - Provision additional Direct connect or VPN connection for high availability.
- One of the usecase: financial or trading application that needs low and consistent latency.
- Provisioning time takes long. 
  - Physical connection needs to follow the AWS Process. 
  - Create a port request.
  - Get letter of authorization and get DataCenter technition to get the cross connection to customer end device at partner location between AWS Direct connect.
  - Arrange transit from the direct connect location to the business premisses.
- VPN over Public VIF at DX enables encryption.

## When and where to choose Direct Connect
- High throughputs.
- Consistent performance and low latency.
- Large amount of data - (Cheaper than VPN if its high vol).
- No contention with existing internet connection.

## Considering both VPN and DX
- VPN as a cheaper HA option for DX.
- VPN as a additinal layer of HA (in addition to two DX).
- If some form of connectivity is needed immediately, VPN provides before the DX connection is live.
- VPN Can be used to add encryption on top of DX (Public VIF VPN).

# Snowball, Snowball Edge, and Snowmobile
- AWS Snowball, Snowball Edge, and Snowmobile are all products designed to allow huge data transfers in and out of AWS. 
- All devides are portable storage devices. 
- This can be used to add in or copy large amount of data. 
- Useful if Large amount of data, limitted internet or not eco viable to transfer large data, or time it takes to get the data transfered.  
## Snowball
- 50 TB to 80TB.
- 1 Gbps with RJ45 or 10Gbps (LR/SR) using a SFP.
- Data encryption using KMS.
- End to end process time is low for the amount of data.
- Larger jobs or multiple location can use multiple snowballs.
- Used for 10TB -> 10 PB (Economical range)

## Snowball Edge
- Additional to Snowball, the snowball edge gets both storage and compute option.
- Used as in same situation as Snowball but for the option where it requires compute.
- A large capacity.
- 1 Gbps with RJ45 or 10/25 Gbps (LR/SR) using a SFP, 45/50/100 Gbps (QSFP+)
- Compute can be used for local instances or lambda functionality, local IoT, for data processing priot to ingestion into AWS.
- Three versions:
  - Edge storage optimized: 80TB, 24vCPU, 32G RAM
  - Edge compute optimized: 100TB + 7.68 TB NVMe, 52vCPUs, 208G RAM
  - Edge compute optimized with GPU.

## Snowmobile
- Portable storage data center - A shipping container on a semi truck.
- Available with special order.
- 100 PB.
- Not economical for Sub 10PB and where multiple locations are required.

# Data and DB Migration

## Storage Gateway
- It is a virtual appliance used for data center extensions or migrations.
- It is a service that connects to on prem DC with AWS Storage services.
- Storage gateway connects to Public Endpoint.
- Benefits are:
  - it allows to migrate the entire or part of storage to AWS.
  - extends the storage capabilities to AWS.
- Storage gateways are the virtual appliance running on a host platform.
  - It is downloaded and installed on DC or onprem instances.
  - It can install on any location that has internet connection.
- Storage Gateway is capable of running in three modes:
  - File gateway
    - Choosing this option you get a virtual image that can be installed at on Prem.
    - We get a SMB Share, and can be used to upload and download the files.
    - Any data added to the SMB share will get saved to S3.
    - Helps to migrate data, or use as a storage place, or unlimitted storage at on Prem.
    - It stores files, using SMB and stores data at the S3.
  - Volume gateway
    - You create an access volumes, and accessed over iscsi protocol.
    - Iscsi is used over NAS or SAN product.
    - Its a network attached storage.
    - Anything that uses the iscsi can use the storage.
    - It is the block devices and the volume needs to be mounted to access.
    - Data is stored in S3, same like snapshot based backup on S3.
    - Data is moved to AWS by taking snapshot to S3, and copy that snapshot as volume to mount on EC2.
  - Tape gateway
    - Virtual Tape library (VTL), it is presented over ISCSI which supports tape drive based backups.
    - Costly and admin overhead.
    - Any data backed up are stored on S3.
    - Moving tape to tapeshelf, migrates data on S3 to Glacier.

## Database migration service
- Database Migration service AWS DMS is a service to migrate **relational database**.
- Migrate to and from any locations with network connectivity to AWS. 
- Traditionally two ways:
  - Backup and restore method.
    - Stop all input and output on DB. 
    - DB backup is dumped to and created new db from it.
    - Change app to use new DB.
    - Admin overhead and takes downtime.
    - Takes more time depending on DB size.
  - Replication:
    - DB is replicated to a destination.
    - Once all the replication is done (brings to parity) 
    - Config app to use the new endpoint.
    - Fairly complex and admin intensive.
    - Production and large dbs are used this way.
- AWS DMS performs the replication as a service.
- It is a replication instance created and its function is to migrate the database to a destination.
- Application can continue to work on Source and at end migrate to Target.
- Oracle, Microsoft SQL, Aurora, SAP, MongoDB, MariaDB.
- Data can be synced to most of the above engines as well as RedShift, S3 and DDB.
- AWS Schema Conversion Tool AWS SCT can be used to transform between different database engines as part of migration.
  - Transforms structure of DB change while converting data between different DB engines. 
- DMS can be used:
  - Migrate
  - Want to scaleup existing Database.
  - Schema conversion tool to move data between two diff DB engines.
  - can be used to Partial/sunset of data migration.
  - Migration with little to no admin overhead, as a service. 

# Identity Federation (IDF) and Signle sign on (SSO)
- ID federation (IDF) is an architecture where identites of an external identity provider (IDP) are recognized.
- SSO is where the credentials of an external iddentity are used to allow access to a local system.
- Example: Mobile app signing with Facebook or Google account. While allowing the access, the process followed by the applicaiton is called identity federation.

Types of IDF:
  - **Cross account roles:** A remote account IDP (In this case remote IAM Role) is allowed to assume a rile and access your account's resources.
    - Here you are allowing the external identity to allow access to your account.
  - **SMAL 2.0 IDF**: An on prem or AWS hosted directory service instance is configured to allow AD users to login to AWS.
    - Integrates different ID providers with application.
  - **Web Identity Federation:** IDPs such as Google, Amazon and Facebook are allowed to assume role and access resources in the account.
- Cognito and Secure Token Service (STS) are used for SAML and Web Identity federation.
  - A federated identity is verified using an external IDP and by proving the identity (using a token or assertion of some kind) is allowed to swap that ID for a temporary AWS Cred by assuming a role.
  - Cognito is a broker for SSO or IDF which provides a ID pool.
  - Cognito allows to merge different identity and provide it as a single user. 
- You can never access AWS resources without an AWS Identity and if you are using an different IDP you have to perform an exchange and of token, which is the basics of IDF.
## AWS Single SignOn with AD (SAML 2.0 Federation).
![Alt text](/pic/ssoad.png?raw=true "AWS Single SignOn with AD arch diagram")
- Loging into AWS using internal AD Identity workflow as below.
  - Login to ADFS using the AD credentials (if local workstation already logged in it might use SSO).
  - ADFS returns the SAML Assertion (It is a token that proves that you are yourself).
  - Now SAML asserstion is delivered to the AWS SSO endpoint. This is the endpoint configured inside the AWS if you want to use SAML SSO federation.
  - The SSO endpoint checks the SAML asserstion with ADFS if its coming from same ADFS and validates the same. There is a trust between ADFS and AWS SSO endpoint.
  - At this point AWS SSO returns a URL that redirects you to AWS Console and you get logged in.
    - Prior to that, in the backend, the SSO endpoint communicates with STS and using the preconfigured Role abstracted from SAML assertion, it generates the Temporary sec credentials for the IAM Role.
    - The URL is modified to incluide the temporary sec credential hence the user is able to successfully login.

## Web Identity Federation
![Alt text](/pic/webIdfederation.png?raw=true "Web Identity Federation arch diagram")
- Lets assume you have an app on mobile app/Web app and you want to login and prompted with Google/Facebook or any other ID provider.
- When you login, you will redirect to Google, and it provides a Token.
- This Token is passed by mobile application either directly to STS or Amazon Cognito. It basically request to assume the Role. 
  - The role assumption happens and gets back a temp sec credentials to directly access AWS Resources.
- (A tool to play with Web Identity Federation)[https://web-identity-federation-playground.s3.amazonaws.com/index.html)

# Simple Notification Service
![Alt text](/pic/sns.png?raw=true "SNS")
- It is a publisher -> Topic <- subscriber based service. 
- So the base entitity in SNS is a topic and various entities can send messages to this topic called publishers.
- The other end of the topic is a subscriber, that recieves the message. 
- CloudWatch sending Alarm, CFN sending event notice, and almost any services can send notification to SNS.
- It is a regional service and fully recielient to the availabilities in the region.
- SNS has an endpoint accessible via Public or VPC endpoints.
- SNS supports encryption at rest and transit.
- A topic can be set with appropriate resource policies.
- 256KB size of message could be send to a Topic.
- The subscribers can be HTTP/S, Email, Email-json, SQS, Lambda, SMS (celluar messages) and Platform application endpoint.
- Identical payload for all delivery 
  - While sending message defines what payload to be send to all protocols subscribed
- Custom payload for each delivery
  - While sending message defines what payload to be send to each protocols subscribed
- SNS is capable of sending push notification to all mobile platforms.
- SNS filter could be created to notify certain group of engineers.
- Topic for SQS fanout (Explained with a scenario)
  - People can upload video need to send message to a topic.
  - A multiple queue subscribing to the queue which receieves the message.
  - Each queues gets the identical message, and perform a job of decoding video to different bit rates.


# Simple Queue Service
- Almost similar to the SNS architecture, and can add complementary to the SNS service.
- Fully managed HA message queues, used for inter process, inter server or inter service messaging. 
- SQS is used to add a message to a queue, and one of the process or service can retrieve the message.
- Allowing Asyncronosly to talk between two components between applications.
- Example, once upload a file to S3, send a message to SQS so worker can go and pull the message and perform a job.
- Each message can contain upto 256 KB, if the message is more than 256 KB then can have the data residing on S3 and the SQS message can just be the link to S3.
- Messages from the queue are pulled by **Polling**.
  - Two types of polling.
    - Short polling.
      - Is a single API queue to check for any messages. If there are messages it will get delivered.
      - The number of messages that can be retrieved is configurable from single message to max of 10 messages.
      - The response to short polling will be
        - 'No messages' if there are no messages
        - Messages that are available in the queue at that point upto 10.
        - A constant API loop needs to be used to pull messages always, costing the API Limit.
    - Long polling. 
      - It performs the same message checks but Waits for messages for a given WaitTimeSeconds.
        - no Need of a loop polling as during the waitTime it will get the message delivered. Saves No Message API calls.
        - It waits for any messages until the waitTimeSeconds is expired.
- Once you receive a message using either Short polling or Long polling the messages will be Hidden from the queue.
  - The message is hidden for the visibilityTimeOut (30 Sec) period. 
  - When it expires the message returns to the queue for other polling service.
- Once the message is processed, The message has to be deleted by the service.
  - This is the way the queues in the message gets HA and automatic retry.
- SQS queue are Two types
  - Standard
    - Standard queues are distributed and scalable to nearly unlimitted message volume. 
    - The order is not guaranteed, but with best-effort.
    - Certain circumstances, there will be a duplicate message received.
    - However standard queue guarantees to be delivered at least once.
    - Good performance, scalability.
  - FIFO (First in and First out)
    - They guaranteed message once and once only.
    - Order of the message added is the order that you receive. 
    - Limited to ~3000 messages per sec with batching.
    - 300 by default.
- Architecture    
![Alt text](/pic/sqs.png?raw=true "SQS")
- Used to decouple the applications. 
- In above example, the front end and backend are decoupled.
  - Each of them scales and will fail independedly.
  - Based on the messages in the queue the worker pool instances can be scaled.
- Hands on experience
```
aws sqs get-queue-attributes --queue-url https://URL --attribute-names All
aws sqs send-message --queue-url https://URL --message-body "INSERTMESSAGE"
aws sqs receive-message --queue-url https://URL
aws sqs delete-message --queue-url https://URL --receipt-handle "INSERTHANDLE"
aws sqs receive-message --wait-time-seconds 10 --max-number-of-messages 10 --queue-url https://URL
aws sqs --region us-east-1 receive-message --wait-time-seconds 10 --max-number-of-messages 10 --queue-url https://URL
aws sqs delete-message --queue-url https://URL --receipt-handle "INSERTHANDLE"
```
- The messages once polled are always hidden, until the visibility timeout. Using receipt handle it has to be deleted.
- A short poll returns immediately and long poll waits until the time.
- A lambda can be triggered when a message is added to the queue.

# Elastic Trancoder.
- Service allows to convert media from one format to another.
- Pay for the compute resource used during the conversion.
- If a 4k video is uploaded and need different formats, the transcoder can convert it.
- Create pipleline for configuring the transcode process.
  - Specify source S3 bucket and output bucket to copy the files once transcoded.
  - Jobs are added to the pipeline.
  - A given job can output one or more destination files.
  - Presets has different encoding formats, device compatability, output formats and the resolution.
  - An event driven pipeline can be created (Serverless) for a transcoding job. Once the file is on S3 start the job.
- Multiple pipelines are added according the priority.

# Analytics
## AWS Athena
- Athena helps to query huge data sets stored in S3.
- Only paid for the data volume queried for the service.
- Traditional database engine needs to create the table structure and data sctructure in advance, which is called the schema.
  - Once the schema is in place the data has to be inside the schema.
  - Issues are
    - Database schema cannot easily change.
    - Maintain the database and schema even if the data is not being quiried.
- Athena tries to address these two issues.
- Athena handles things differents, the data stays in S3 in original format.
- Supports XML, JSON, CSV/TSV, ARVO, ORC, PARQUET etc..
- Main benefit is that all data can be on S3.
- Amazon Athena is an interactive query service that utilizes schema-on-read mechanism.
  - Schema-on-read:
    - You can define the schema in advance.
    - In this we define the table attribute and structure on what you want the data to be looked.
    - Schema not only defines what structure it like on S3 but how exactly how we want it to look.
    - Schema is only used when performing the query.
      - it is like define a virtual table created and reads data through the virtual table.
    - This massively reduce the admin overhead. As no need of data manupulation when the data is added to Athena, Just point to S3.
- Athena uses serverless data processing engine.
  - It gathers the data, reads using the schema and present it to you.
- Athena dont make any modification to the source data.
- Example usecase: Cloud Trail data analysis using Athena.
  - From CloudTrail can use advanced query option to create the table (which acts as a lense). This is the method of creating Schema.
- Billing is based on the amount of data it queiried.
- Useful for adhoc situation, querying large dataset infrequently. 

## Elastic MapReduce (EMR)
- Is a product allows to perform the analysis of semi-structured and unstructured data.
- It is based on the Apache Hadoop framework, and service is delivered as a Managed Cluster using EC2 instances.
- The EMR cluster has Marster Nodes and Core Nodes running on Managed EC2 instances.
  - **Master node** controller manages HDFS, allocation of work etc.
  - Master node never be used as a spot instances (can only be used for short lived clusters). 
  - **Core nodes** manages the data for the HDFS shared filesystem. 
  - Failure of core nodes can cause storage instability and any job or part of a big job running on the system fails.
  - **Task nodes** they only runs tasks. It has no role in cluster management. 
  - Task nodes failures can be recovered.
- S3 uses as data store. EMRFS the whole data is residing on S3.
- EMR is used for huge scale log analysis, indexing, machine learning, financial analysis, simulations, bioinformatics and many other large scale application.
  - It process huge sets of data.
  - The cluster split the works and allocates portions to the nodes. 
  - As its cluster it needs a shared filesystem. Traditionally in Hadoop it was using HDFS. The filesystem existed to the life time of cluster.
  - EMRFS cluster file system is an enhancement for filestem specific to EMR, based on S3.
  - Data exists on EMRFS even if the cluster is unavailable. 
  - This is one of the benefits and it can be used for ad hoc work. 
- When to use it?
  - It is ondemand billing.
  - Used for short lived tasks.
  - Used for large scale data analytics.
  - Any manupulation, calculation of data EMR is used.
  - Remember query can be achieved by Athena.

##  Kinesis and Firehose
- Is scalable and resilient streaming service from AWS>
- It is designed to ingest large amount of data from hunders, thousands or even millions of producers.
- Consumers can access a rolling window of that data or it can be stored in persistent storage of database products.
- How Kinesis is nothing like SQS:
  - It is designed to allow to process real time data.
  - Example: Imagine millions of IoT sending telemetry to send. 
    - Think about the amoung data being send and need processing, the bandwidth needed, API endpoints and computing powers needed for such infrasctructure and storage.
    - This can be a barrier for scaling up.
    - Think about you delevoped an app, it went viral. Now a million of user tapping telemetry is being tracked by the mobile app and generates large amount of data.
- Kinesis is designed to ingest huge quantity of data in real time.
- It is fully managed service and most scalable service in AWS.
- Architecture    
![Alt text](/pic/kinesis.png?raw=true "Kinesis")
- Producers 
  - Are the things that put data into Kinesis. 
  - Any services that are able to make use of Kinesis API to inject data.
- Consumers 
  - Are the one who can consume data which is added to Kinesis. 
- Kinesis Stream.
  - Is where the producers push data into. 
  - It allows consumptions to consumers. 
  - It include storage for all incoming data with a 24 hour default window and can be increased to seven daus for an additional charge. 
  - Data records are added by producers and read by consimers.
  - A stream provides a rolling 24 hour, the data is not modified or deleted until the data record rolling window.
  - Stream can scale almost infinetly, and is performed using Kinesis Shard. 
- Kinesis Shard.
  - Shard provides capacity to the Stream.
  - Each shard gives one 1MB of injection and 2MB of consumption capacity per Stream.
  - If stream needs more load, add more Shard.
  - All consumers consumes shard. 
  - Ability to scale in or out as Shard can be modified after a stream is created.
- Kinesis Data record.
  - The data that is added by Producers and read by consumers is called Kinesis Data record.
  - A data record can be upto 1 MB in size. 
- Kinesis supports
  - Data Stream
  - Video Stream
- SQS doesnt support one message being processed by many, but Kinesis allows multiple consumers to process.
- Kinesis is not used to decouple the application, but allows large scale application to process the data in the stream rolling time.
- Example data from IoT process the data
  - Lambda of Temperature to report temp.
  - Lambda of Rain predicts rain from the same stream data.
- Kinesis Data Firehose.
  - It can accept record from Stream.
  - It can persistently store data on S3.
  - It can also be stored on RedShift, Elastic Search and Splunk.
  - It can perform Data transformation using SQL query, modify data and store it to S3 or RedShift. 
  - Example, Streaming record from producers reaches Kinesis Stream, and Kinesis Fire hose can be a consumer, who does SQL query and stores data in ElasticSearch/S3.
- Charge for every million payload poll.
  - Payload poll is 25KB of data.

## RedShift
- Is petabyte scale data wareshouse solution.
- Data base is designed for OLAP based application (Online Alalytical Processing).
- OLTP (Online Transaction Processing) which is what most normal db do.
- Update and add individual record is what RDS do. 
- RedShift is used for Dataware housing and Analytics and data is stored in Column.
  - For example: Every ones firstname, surname and everyones age is stored together in same location of physical storage devices.
  - So it is better doing query for large amount of same type of data.
    - Example looking up people who has similar Surname, Age etc. 
- Traditional DB will be costly and time consuming for such scenarios.
- It uses cluster architecture capable of loading and unloading data from S3.
- Kinesis and Firehose can be a product that can store data in RedShift.
- Architecture    
![Alt text](/pic/redshift.png?raw=true "RedShift")
- Leader node 
  - Decides to execute the query and allocates to specific the Slices.
- Compute nodes
  - Each compute nodes has Slices that performes the query.
- It can scale to any load level and desgined to operate in PB.
- Differences between diff analytical tools?
  - **Athena** is used for transactional types of query where data in S3.
    - Same type of query that you do with Relational DB.
    - No need to maintain the DB infra.
  - **EMR** is used to perform analytical and when needs to modify the data.
    - When semi structure or unstructure data needs some modification from one form to another EMR is used.
  - **RedShift**: If the data is processed and one single location that can do a analytical data query, then RedShift is used.
    - Once data is proccessed by different types of tools and need a summariezed analysis of ther data RedShift is used.
    - Reporting, end of month processing (periodic analysis), trends etc.

# Monitoring and Logging
## CloudWatch
- Architecture    
![Alt text](/pic/cw.png?raw=true "CloudWatch")
- CW provides a full suite of metrics collection and monitoring functionality.
- With AWS CW all services send data to CloudWatch which groups together called Metrics and based on Alarms from the metrics could take action.
- Publish data using CW Agents from custom location.
- By default:
  - EC2 instance Network usage, CPU Usage are shown by default(at hypervisor level).
  - CW Agent needs be installed for metrics within the instance (Memory monitoring).
- CW can be thought of a repository service for metrics.
- **Metrics** are a time ordered set of data points.
  - Each of data points or actual value at specific point in time are grouped to form the metrics.
    - Example: CPU Usage at 24:00:00 hrs.
- Frequency of datapoint injection depends on service.
- Data retention is based on granularity:
  - One hour metrics are retained for 455 days.
  - Five minutes metrics for 63 days.
  - One minute metrics for 15 days.
    - *The older the data get the lesser the granularity. Super detail data only matter is short term. The long term will be checked with the trend*.
- Metrics are grouped into **Namespaces**
- Alarm can be created on Metrics taking a action if the alarm is triggered. 
  - Alarms have three states
    - **Insufficient**: Not enough data to judge the state. Alarms start in this state. 
    - **Alarm**: The alarm threshold has been breached. 
    - **Ok**: Alarm has not been breached.
  - Alarms are configured with below key componenents.
    - Metric: the data points over time being measured.
    - Threshold: Exceeding this is bad.
      - Static: You define a condition, if value more or less then alarm.
      - Anomly: CW detects a normal range from the history with a long term data. And if exceeds it triggers anomly.
    - Period: How lond the threshold should be bad before an alarm is triggered. 
      - CloudWatch period is related to its threshold. It is the length of time in which a threshold is surpassed before an alarm is generated.
    - Action: What to do when alarm triggers.
      - SNS
      - ASG
      - EC2
### CloudWatch Logs
- Subset of CW designed to collect and store logs
- Log Event: the time stamp YYYYMMDDHHMMSS together with the RAW Message makes up the LogEvent.
- Log streams: Log events are grouped to Log Stream:
- Log Groups: A log group is a container for log sreams, It controls retentiion, monitoring and access control.
  - Example: /aws/lambda/mylambdafunction
  - Whenever a service sending data to CW, its send to Log Group.
- Inside Log Group -> Log Stream -> Log events 
  Example: Log group of EC2 -> Log Stream of Instance IDs -> Log event of messages. 
- Log group can get exported to S3.
- Steam to AWS and AWS ECS is configured from Log Group. 
- Retention of logs configured.
- Metric filter can be used to filter a string from the log event and create the metric.
  - Example, Create metrics and alarm for a string in /var/log/messages. 
  - Example, Metrics for Application specific strings.
  - Metric filter is created at the Log Group. 
### CloudWatch Events.
- Location to see the event happened in AWS Cloud.
- Events has a near real-time vibility of changes that happen within an AWS Accounts.
- Using rules can match against certain events and deliver those events to a number of supported targets.
- With rules, many AWS Services are natively supported as events sources and deliver the events directly.
- For other CW allows event pattern matching against CloudTrail events.
- Additional rules support scheduled events as sources allowing a cron style function for periodically passing events to targets.
- Example of event targets:
  - EC2 instances
  - Lambda
  - Step function state machines
  - SNS Topics
  - SQS Queues
  - And many more.
- Example:
  - 1. Daily at 12.00AM -> invoke Lambda -> Update DDB Table
  - 2. CloudTrail Stopping event -> Lambda function re-enable Ctrail  
- Difference between Ctrail and CW Events is that CW events can do something based on a event, But ctrail can only monitor.
- Apart form Ctrail, CW Event can see the issue as it occurs (No delay)


## CloudTrail
- Is a governance, compliance, risk governance and auditing service.
- Records activites within AWS Account. 
- One of the first thing to be enabled.
- By default the CloudTrail is enabled on all new accounts by 90 days.
- Older AWS Account, needs to create a new trail and create it seperately.
- All AWS API calls are logged.
- By default 90 days old events are available in Event History.
- **Trail** inside the CloudTrail defines exactly what is logged and where it want to store the data.
  - Trail is per region configuration.
  - Output location:
  - Management events: are associated with management operations (All AWS Api events). 
  - Data Events: Provides insights to the resource operations with in a service. Example S3 and Lambda.
  - Trail can be stored at a S3 bucket.
  - While delivering logs to S3, we can also configure to delivery CloudTrail to CloudWatch in parallel.
    - This allows to create a metrics fileter and alarm for certain type of AWS API events.
- Logs are delievered in batches to S3 and CloudWatch hence there will be a bit delay.

## VPC Flow logs.
- VPC Flow logs allow you to capture metada about the traffic flowing in and out of networking interfaces within a VPC.
- Flow logs can be placed on a specific network interface, A Subnet or an entire VPC **to capture metadata from the capture point and anything within it**. 
- Flow logs aren't realtime, it doesn't capture actual data but only metadata of the traffic.
- Flow log are attached to VPC, then entire interface in the VPC is monitored.
  - If at Subnet level only interfaces at the subnet is monitored.
  - Creating the flow log at a level, it captures the logs down in the hierarchy.
- Architecture
![Alt text](/pic/vpcflowlog.png?raw=true "VPCFlowLog")
- Flow logs capture 
  - Order of VPC Flow log format as follow:
    - `account-id, inteface-id, src ip, dst Ip, src port, dst port, protocol, numbe of packets, bytes, start and end time, Allowed or rejected action and Flow log log-status`.
  - It is not used sniff the traffic or contect of the traffic, just used the metadata to get above information.
- Creating the Flow logs allows to choose the destination - S3 or CloudWatch.
- In Cloudwatch the log group includes all the interfaces as log stream.
- VPC Flow logs can't be used for "Realtime" analytics.
- Windows License activation, 169.254.168.254 address, Amazon DNS Traffic, DHCP traffic and VPC Router traffics are Not captured.
### Analyze VPC Flow Logs Data in Athena
##### Create the Athena table:
```
    CREATE EXTERNAL TABLE IF NOT EXISTS default.vpc_flow_logs (
      version int,
      account string,
      interfaceid string,
      sourceaddress string,
      destinationaddress string,
      sourceport int,
      destinationport int,
      protocol int,
      numpackets int,
      numbytes bigint,
      starttime int,
      endtime int,
      action string,
      logstatus string
    )  
    PARTITIONED BY (dt string)
    ROW FORMAT DELIMITED
    FIELDS TERMINATED BY ' '
    LOCATION 's3://{your_log_bucket}/AWSLogs/{account_id}/vpcflowlogs/us-east-1/'
    TBLPROPERTIES ("skip.header.line.count"="1");
```

##### Create partitions to be able to read the data:
```
    ALTER TABLE default.vpc_flow_logs
    ADD PARTITION (dt='{Year}-{Month}-{Day}')
    location 's3://{your_log_bucket}/AWSLogs/{account_id}/vpcflowlogs/us-east-1/{Year}/{Month}/{Day}';
```
##### Run the following query in a new query window:
```
    SELECT day_of_week(from_iso8601_timestamp(dt)) AS
      day,
      dt,
      interfaceid,
      sourceaddress,
      destinationport,
      action,
      protocol
    FROM vpc_flow_logs
    WHERE action = 'REJECT' AND protocol = 6
    order by sourceaddress
    LIMIT 100;
```
# AWS KMS (Key management service)
- KMS Allows to create modify and delete customer Master Keys.
- AWS KMS provides regional security Ket management and encryption and decryption services.
- KMS is FIPS 140-2 Level 2 validated and certain aspects support Level 3.. 
- KMS can use CloudHSM via Custom Key Stores (FIPS 140-2 Level 3)
- KMS manages customer master keys (CMK), which are created in a region and never leave the region or KMS.
- They can encrypt or decrypt data **utp 4 KB**.
- By default KMS is capable of performing cyrptographic operations on Data upto 4 KB in size using CMKs
- Any form of encryption in AWS uses KMS.
- Types of CMK
  - AWS Owned CMK.
    - Cannot view
    - Cannot Manage
    - Not dedicated to AWS Account. 
    - Keys used by AWS on a shared basis across many accounts.
  - AWS Managed CMK.
    - Can view
    - But cannot Manage
    - It is dedicated to the Account 
    - It is used by default if you pick encryption within most AWS Services and formatted as aws/service-name.
    - Only service they belong can use them directly.
  - Customer Managed.
    - Created by customer.
    - Can view
    - can Manage 
    - Dedicated to the account.
    - Certain services allow you to pick a CMK you manage. Customer managed keys allow key rotation configuration.
    - They can be controlled via Key polices and enable and disable.
    - If we are configuring an encryption for service in AWS then CMK is used, as it allows to make changes.
- Key created by default trust everyone in the account.
- KMS uses base 64 encoded text for any operations to send or receive data to KMS.
- When decrypting dont have to specify the CMK Key ID. This is because, whenever you have the encrypted data - inside that it has the link back to the CMK that is used to encrypt the data.
- KMS Re-Encrypt:
  - If customer has access to files, but dont want to see the data.
  - KMS can run re-encrypt, to encrypt plain text.
- KMS can generate DEK (Data encryption Keys) using CMK to encrypt large amount (> 4KB data) file. 
- Hand on demo Customer Managed Keys
```
aws kms create-key --description "LA KMS DEMO CMK"
aws kms create-alias --target-key-id XXX --alias-name "alias/lakmsdemo" --region us-east-1
echo "this is a secret message" > topsecret.txt
aws kms encrypt --key-id KEYID --plaintext file://topsecret.txt --output text --query CiphertextBlob 
aws kms encrypt --key-id KEYID --plaintext file://topsecret.txt --output text --query CiphertextBlob | base64 --decode > topsecret.encrypted
aws kms decrypt --ciphertext-blob fileb://topsecret.encrypted --output text --query Plaintext | base64 --decode 
aws kms generate-data-key --key-id KEYID --key-spec AES_256 --region us-east-1
```
- In this example, a sample text is encrypted and decrypted using the CMK.
- KMS has Custom Key store.
  - KMS is capable of Interacting with CloudHSM, so it can use FIPS 140-2 Level 3 encryption.

# Beanstalk
- When to select?
  - Low level infra control.
  - Code needs to be designed for Beanstalk. 
  - No admin overhead, absolute no admin overhead with all above critera. 
# OpsWorks
- Designed for Infra engineer not for delveloper.

# Exam Preperation
- re:Invent Videos 1xx, 2xx, 3xx or 4xx videos. 
  - Suggest 4xx videos
    - Compute
    - Storage
    - Network
    - Database
- [Exam registration Link](https://aws.amazon.com/certification/certified-solutions-architect-associate/) 
- [Sample Questions](https://d1.awsstatic.com/training-and-certification/docs/AWS_Certified_Solutions_Architect_Associate_Sample_Questions.pdf)
- [Exam Guide](https://d1.awsstatic.com/training-and-certification/docs-sa-assoc/AWS_Certified_Solutions_Architect_Associate-Exam_Guide_EN_1.8.pdf)
- [Certification Prep](https://aws.amazon.com/certification/certification-prep/)
- 3 Phase to answer
  - 1 Answer immediately the easy questions.
  - 2 need thoughts, answer and of mark for review and move on.
  - 3 reserve questions. Might be very few, and will have enough time to answer it.
- 130 Minutes
- 65 Questions
- Passing score 720
- 3 yrs validity.
