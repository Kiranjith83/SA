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
``
[ec2-user@ip-172-31-57-48 ~]⎈ : ipcalc -b 10.0.0.0/19
BROADCAST=10.0.31.255
[ec2-user@ip-172-31-57-48 ~]⎈ : ipcalc -b 10.0.32.0/19
BROADCAST=10.0.63.255
[ec2-user@ip-172-31-57-48 ~]⎈ : ipcalc -b 10.0.64.0/19
BROADCAST=10.0.95.255
[ec2-user@ip-172-31-57-48 ~]⎈ : ipcalc -b 10.0.96.0/19
BROADCAST=10.0.127.255
[ec2-user@ip-172-31-57-48 ~]⎈ : ipcalc -b 10.0.128.0/19
BROADCAST=10.0.159.255
[ec2-user@ip-172-31-57-48 ~]⎈ : ipcalc -b 10.0.160.0/19
BROADCAST=10.0.191.255
[ec2-user@ip-172-31-57-48 ~]⎈ : ipcalc -b 10.0.192.0/19
BROADCAST=10.0.223.255
[ec2-user@ip-172-31-57-48 ~]⎈ : ipcalc -b 10.0.224.0/19
BROADCAST=10.0.255.255
```