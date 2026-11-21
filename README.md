# aws-ec2-nginx-web-serv-dep
# AWS EC2 — Nginx Web Server Deployment

## Project Overview

Deployed and configured an Nginx web server on an Ubuntu EC2 instance in AWS. Hosted a custom HTML website, configured HTTP access, monitored web traffic, and performed service troubleshooting.

## Technologies Used

- AWS EC2, VPC, Security Groups, Internet Gateway
- Ubuntu Server 24.04 LTS
- Nginx
- Linux systemd
- HTTP and SSH
- curl and Linux logging utilities

## Architecture

Browser → Internet Gateway → Public Subnet → EC2 (Ubuntu + Nginx) → HTML Website

**AWS Region:** us-east-2 (Ohio)

## Implementation

1. Started an existing Ubuntu EC2 instance.
2. Resolved an SSH timeout by updating the Security Group to allow SSH from the current public IP.
3. Installed and started Nginx.
4. Allowed inbound HTTP traffic on TCP port 80.
5. Created and deployed a custom HTML homepage.
6. Inspected Nginx access logs and identified HTTP status codes.
7. Used curl to test local HTTP connectivity.
8. Simulated a service outage by stopping Nginx, diagnosed the failure, and restored the service.
9. Verified Nginx was active and enabled for automatic startup.

## Troubleshooting Experience

**Issue 1: SSH Connection Timeout**

**Cause:** The Security Group's SSH rule permitted an outdated client public IP address.

**Resolution:** Updated the inbound SSH rule to allow TCP port 22 from the current IP address.

**Issue 2: HTTP 404 Not Found**

Requested a nonexistent page and confirmed that Nginx was reachable but could not find the resource.

**Issue 3: Web Server Outage**

Stopped Nginx intentionally and verified that localhost HTTP connectivity failed. Restarted the service and confirmed that HTTP returned 200 OK.

## Verification Commands

```bash
sudo systemctl status nginx
sudo systemctl is-enabled nginx
sudo systemctl is-active nginx
curl -I http://localhost
sudo tail -n 10 /var/log/nginx/access.log
```

## Security Considerations

- SSH restricted to an authorized client IP.
- HTTP port 80 opened for testing.
- SSH private keys and AWS credentials excluded from the repository.
- HTTPS is not yet configured; this is a learning environment rather than a production deployment.

## Project Outcome

Successfully deployed, tested, and troubleshot an AWS-hosted website while gaining practical experience in Linux system administration, HTTP networking, Security Groups, and Nginx service management.

## Future Improvements

- Configure HTTPS with a domain name.
- Automate deployment using Bash or Terraform.
- Implement monitoring with Amazon CloudWatch.
- Containerize a web application using Docker.
