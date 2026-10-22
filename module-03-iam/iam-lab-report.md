AWS IAM Lab: Policy Evaluation, Implicit Deny, and Explicit Deny
Environment: AWS Free Tier account (training lab)
Service: AWS Identity and Access Management (IAM)
Testing Tool: IAM Policy Simulator
Policy: AmazonS3ReadOnlyAccess
Objective
Evaluate how AWS IAM determines whether an identity is allowed or denied permission to perform Amazon S3 actions and observe how an explicit Deny affects an existing Allow permission.
What I Tested
I tested an IAM user with the AWS-managed AmazonS3ReadOnlyAccess policy attached. Using the IAM Policy Simulator, I evaluated the s3:GetObject and s3:PutObject actions before and after applying an explicit Deny policy.
Results
IAM Action | Before Explicit Deny | After Explicit Deny
s3:GetObject | Allowed | Denied (Explicit Deny)
s3:PutObject | Denied (Implicit Deny) | Denied (Implicit Deny)
Evaluation Logic
1. Implicit Deny: AWS IAM denies requests by default when no applicable policy grants the required permission.
2. Explicit Allow: An applicable Allow statement grants permission, subject to the overall policy evaluation process.
3. Explicit Deny: An applicable Deny statement overrides an Allow statement, resulting in a denied request.
4. Least Privilege: Access should be restricted to the minimum permissions required to perform a task.
Key Takeaways
• IAM permissions are determined by evaluating the policies applicable to a request.
• An existing Allow does not guarantee access if another applicable policy explicitly denies the action.
• An implicit Deny and an explicit Deny both result in denied access, but they have different policy evaluation causes.
• The IAM Policy Simulator helps validate authorization logic before testing against a live AWS resource.
Cleanup
Deleted the temporary IAM test user after completing the lab.
