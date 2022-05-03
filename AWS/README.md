# AWS NOTE

---
## EC2
- RDS Region must be same as EC2 Region
- Set 443 Port Load Balancer & Web Server Port(FastAPI:8000) Target Group
  - Due to interception of CLIENT<->Server request, ELB adds `x-fowarded-for`: `client-ip-address` into request header
- Set Security Group
---
## ROUTE 53
`HTTPS`
- Create Domain
- Create CNAME Record with Certificate Manager
- Create A Record with Load Balancer
---
## IAM
1. Create User
2. Add Permission Policy
3. ```
   - awscli
   $aws configure
   aws_access_key_id = MY-KEY
   aws_secret_access_key = MY-SECRET-KEY
   ```
---
## CLOUDWATCH
> SET IAM
> - Add Permission CloudWatchLogsFullAccess Policy
> - $aws configure(User with CloudWatchLogsFullAccess)

---
## S3
- Bucket Policy
- CORS Policy

> Mount with Goofys
> ```
> install golang, awscli, goofys
> 
> $sudo apt-get install golang
> $sudo apt install awscli
> $sudo wget http://bit.ly/goofys-latest -O /usr/local/bin/goofys
> $sudo chmod 755 /usr/local/bin/goofys
> $aws configure(User with AmazonS3FullAccess)
> 
> # MOUNT
> $goofys [bucket name] [target directory]
> # UNMOUNT
> $umount [target directory]
> # check mount
> $df -h
> ```
