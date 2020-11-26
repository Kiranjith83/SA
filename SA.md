# Shared responsibility security model.

# Service models.
 - Iaas
 - Paas
 - Saas

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

# IAM
 - Root account to have MFA to enabled. 

# Billing 
 - Create Billing alarm.

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