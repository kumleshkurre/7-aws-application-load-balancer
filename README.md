# AWS Elastic Load Balancing (Application Load Balancer)

### 📌 Overview
- This project demonstrates how to configure an AWS Application Load Balancer (ALB) to distribute HTTP traffic across two Amazon EC2 instances running an Apache web server.
---
```
User Request
      |
      v
Application Load Balancer (ALB)
      |
-------------------------
|                       |
server1 (EC2)       server2 (EC2)
```
---

## 🚀 EC2 Instance Setup
- Instances: `server1, server2`
- OS: Amazon Linux
- Security Group:
- SSH (22)
- HTTP (80)
- Web Server: Apache (httpd)
```
User Data Script
#!/bin/bash
sudo yum update -y
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd

echo "<html>
<h1>Welcome to Apache Web Server - $(hostname)</h1>
</html>" > /var/www/html/index.html
```
---

## ⚖ Application Load Balancer Setup
- Type: Application Load Balancer
- Name: my-webserver-lb
- IP Type: IPv4
- Security Group:
- HTTP (80) – Anywhere
- HTTPS (443) – Anywhere
- 🎯 Target Group
- Name: mywebserver-lb-tg
- Target Type: Instance
- Protocol/Port: HTTP / 80
- Registered Targets: `server1, server2`

## 🌐 Testing
- Copy the Load Balancer DNS name
- Open it in a browser
- Refresh multiple times to see responses from different instances
---

## 🛠 Troubleshooting (If Website Not Running)
- Go to EC2 → Load Balancers
- Select your Load Balancer
- Go to Resource Map
- Click Target Groups
- Click Register Targets
- Select: `server1 server2`
- Click Include as pending below
- Click Register pending targets
- ⏳ Wait 1–2 minutes and refresh browser
✅ Server will start working
---

## 📌 Conclusion
- Application Load Balancer automatically traffic distribute 
- High Availability aur Fault Tolerance m

 
---

  ## 👨‍💻 Author

**Kumlesh Kurre**
💼 IT Support & Network Engineer

⭐ If you find this guide helpful, don’t forget to star ⭐ the GitHub repository!

**Purpose:** AWS Learning & Practice 🚀
