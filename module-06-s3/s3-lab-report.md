S3 Lab: Access Control, Versioning, and Troubleshooting
Environment: AWS Free plan account (training lab, not production)
What I tested:
A private bucket with versioning, a presigned URL, the AWS CLI in CloudShell, and a bucket policy with an explicit Deny.
Results:
• Open Object URL anonymously: AccessDenied because the bucket is private.
• Open presigned URL: Worked, then expired because it only gives temporary access.
• Delete file with versioning on: A delete marker was added and old versions were kept because versioning preserves file history.
• Upload after explicit Deny: AccessDenied because a Deny rule in the bucket policy blocks everyone.
Error guide:
• NoSuchBucket: This means the bucket name is wrong, or it exists in another Region or AWS account.
• NoSuchKey: This means the file name, spelling, capitalization, or folder path is wrong.
• AccessDenied: This means an AWS policy is blocking the request, and you must read the error message to see which policy is closed.
Cleanup:
I emptied and deleted the bucket from the S3 console, ran the delete commands for the text files inside CloudShell, and checked the Billing dashboard.
What I learned:
I learned that an explicit Deny rule in a bucket policy completely overrides any other permission and instantly blocks access. I also learned that turning on S3 versioning protects data from accidental deletion by hiding the original files under a delete marker instead of permanently erasing them. Finally, I discovered that AWS CloudShell lets me securely run CLI commands and upload files directly inside my browser without storing sensitive security keys on my personal laptop.
Would you like me to generate your ticket reply file using this same simple and clear layout next?
