Project 1: Deploy and Troubleshoot a Cloud Server

Environment: AWS Free Tier (Training Lab)

Objective

Launch a Linux server on AWS, connect securely, host a web page, troubleshoot common issues, and clean up resources.

Architecture

Internet → Security Group (Ports 22 and 80) → EC2 Instance → EBS Volume

Implementation

1. Launched an Amazon Linux 2023 EC2 instance.
2. Connected to the instance securely using SSH and a key pair.
3. Installed and started the Apache web server.
4. Verified that the hosted web page loaded successfully in a browser.

Troubleshooting

Issue 1: Connection Refused

Evidence: The Apache (httpd) service was inactive.

Cause: The web server was stopped.

Solution: Started the Apache service and verified that the page was accessible.

Issue 2: Connection Timed Out

Evidence: The security group had no inbound HTTP rule.

Cause: Traffic on port 80 was blocked.

Solution: Added an inbound rule allowing HTTP traffic on port 80 and tested the page again.

Cleanup and Cost Management

Terminated the EC2 instance, verified that its EBS volume was deleted, and deleted the associated key pair.

Key Takeaways

This project taught me how to identify and troubleshoot common cloud server issues using evidence rather than guesswork. A connection refusal helped me identify a stopped web server, while a connection timeout led me to investigate the security group rules.

I also learned the importance of securing access, verifying fixes, and removing unused resources to reduce the risk of unexpected AWS charges.
