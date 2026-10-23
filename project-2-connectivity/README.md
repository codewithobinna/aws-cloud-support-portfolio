Project 2: Diagnose a Cloud Connectivity Failure

Environment: AWS Free Tier training lab (non-production).

The goal is to build a small VPC network, deploy a working web server, deliberately create three network failures, and find and fix each problem using evidence.

Architecture: Internet → Internet Gateway → Route Table → Network ACL → Security Group → EC2 Web Server

Method

1. Checked the EC2 instance state and confirmed that all status checks passed.
2. Connected to the server and used `curl localhost` to verify that the web service was working locally.
3. Checked the security group, route table, and network ACL to identify where traffic was being blocked.

Findings and Fixes

Issue 1: The Web Page Times Out, but the Local Test Works

Evidence: The security group had no inbound rule for HTTP traffic on port 80.

Root Cause: The server was running, but the security group was blocking incoming web traffic.

Fix: Added an inbound HTTP rule allowing traffic on port 80 from anywhere.

Issue 2: The Web Page Times Out, Even Though the Security Group Allows Traffic

Evidence: Network ACL rule 90 denied traffic on port 80.

Root Cause: Network ACL rules are evaluated in ascending numerical order. The deny rule blocked the traffic before a later allow rule could take effect.

Fix: Removed the conflicting deny rule and verified the connection again.

Issue 3: Both the Web Page and SSH Connection Time Out

Evidence: The route table was missing the 0.0.0.0/0 route to the internet gateway.

Root Cause: The subnet had no default route for sending internet-bound traffic through the internet gateway.

Fix: Restored the default route to the internet gateway and tested connectivity again.

Cleanup and Cost Management

After completing the tests, I terminated the EC2 instance, deleted the custom key pair, and removed the VPC and its associated resources. I also checked the AWS billing page to monitor for any unexpected charges.

What I Learned

This project helped me see that getting a web server online involves more than just starting an instance and installing a web server. At first, I might have assumed that a working server should automatically be accessible from the internet. However, testing with curl localhost showed me that a service can work perfectly inside a server while remaining unreachable from outside.

What I found most useful was learning to investigate each layer instead of randomly changing settings. A missing security group rule, a network ACL deny rule, and a missing route can all prevent access, but they require different fixes.

I also learned to pay attention to the pattern of a failure. When both HTTP and SSH stopped working, it gave me a reason to investigate the shared network path rather than focus only on the web server.

Overall, this project gave me a clearer picture of how AWS networking works and taught me to approach connectivity problems with patience, evidence, and a step-by-step process.
