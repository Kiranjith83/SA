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
   - Application session state is the data that rep what customer is doing. What they choosen, what they selected. 
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
  - Encryption
    - At rest
      - Server side encryption.
         - SSE-S3
         - SSE-KMS
         - SSE-C
      - Client side encryption.
        - Encrypt and upload to S3.
    - At transit
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

# Subnetting.

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