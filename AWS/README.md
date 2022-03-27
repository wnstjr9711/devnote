# AWS NOTE

---
## EC2
- RDS Region must be same as EC2 Region
- Set 443 Port Load Balancer & Web Server Port(FastAPI:8000) Target Group
- Set Security Group
---
## ROUTE 53

`HTTPS`
- Create Domain
- Create CNAME Record with Certificate Manager
- Create A Record with Load Balancer
---
## CLOUDWATCH
- Logging
---
## S3
- Bucket Policy
- CORS Policy


- Mount with Goofys
```ShellSession
install golang, awscli, goofys

$sudo apt-get install golang
$sudo apt install awscli
$aws configure
aws_access_key_id = MY-KEY
aws_secret_access_key = MY-SECRET-KEY

$sudo wget http://bit.ly/goofys-latest -O /usr/local/bin/goofys
$sudo chmod 755 /usr/local/bin/goofys

# MOUNT
$goofys [bucket name] [target directory]
# UNMOUNT
$umount [target directory]
# check mount
$df -h
```