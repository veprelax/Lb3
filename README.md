Виконала самостійно Слобожан Софія РПЗ 24-А

## 1. Key Concepts and Terms (from Lesson 1)

### Main Service Categories
- **Compute**: EC2, Lambda, Elastic Beanstalk.
- **Storage**: S3, EBS, Glacier.
- **Database**: RDS, DynamoDB, Aurora.
- **Networking & Content Delivery**: VPC, Route 53, CloudFront.
- **Security, Identity & Compliance**: IAM, KMS, Shield.
- **Management & Monitoring**: CloudWatch, CloudTrail, AWS Config.

### Key Terms
- **Region**: A geographic area where AWS resources are hosted (e.g., us-east-1).
- **Availability Zone**: Isolated locations within a region for high availability.
- **Elasticity**: The ability to scale resources up or down automatically based on demand.
- **Pay-as-you-go**: Billing model where you pay only for the resources you use.
- **AWS Free Tier**: Free usage limits for new accounts to experiment with services.

## 2. Purpose of MFA and How to Configure It (from Lesson 2)

MFA (Multi-Factor Authentication) adds an extra layer of security to the AWS account by requiring an additional verification factor beyond username and password, such as a time-based code or hardware token.

### Setup Methods
1. **Virtual MFA device**: Use apps like Google Authenticator, Authy, or AWS Virtual MFA to generate codes.
2. **Hardware MFA token**: Physical device such as YubiKey for generating one-time passwords.
3. **U2F/FIDO2 Security Key**: Modern USB key for hardware-based authentication.

### Configuration Path
- AWS Console → IAM → Users → [Select User] → Security credentials → Assign MFA device.
- Scan the QR code with your MFA app and enter the generated codes to verify.

## 3. Purpose of Amazon Budgets and Configuration Options (from Lesson 2)

Amazon Budgets helps manage and monitor spending in AWS by setting alerts and limits to prevent unexpected costs.

### Configuration Options
- **Cost budget**: Limits on total spending (e.g., alert if monthly spend exceeds $100).
- **Usage budget**: Limits on resource usage (e.g., track EC2 instance hours).
- **Reservation budget**: Monitors reserved instances to ensure optimal utilization.
- **Savings Plans budget**: Tracks savings plan utilization for committed usage discounts.

Setup: AWS Console → Billing → Budgets → Create budget.

## 4. IAM Policy Purpose and Setting Permissions (from Lesson 2)

An IAM Policy is a JSON document that defines specific permissions for users, groups, or roles, specifying what actions are allowed or denied on AWS resources.

### How to Configure Permissions
- Create a user in IAM.
- Attach policies (directly to the user, via a group, or by copying from an existing user).
- Define key elements:
  - **Action**: The specific AWS actions (e.g., "s3:GetObject").
  - **Resource**: The AWS resources affected (e.g., "arn:aws:s3:::my-bucket/*").
  - **Effect**: Allow or Deny.

Follow the Principle of Least Privilege: Grant only the minimum permissions needed.

## 5. Options for Adding IAM Policy When Creating a User

1. **Attach existing policies directly**: Use predefined AWS managed policies (e.g., AdministratorAccess).
2. **Add user to group**: Assign the user to an IAM group that already has attached policies.
3. **Copy permissions from existing user**: Duplicate the permissions of another user during creation.
4. **Attach custom policy**: Create and attach your own JSON-based policy for tailored access.

## 6. Writing and Applying IAM Policies (from Lesson 3)

IAM policies are written in JSON and applied to users, groups, or roles to grant or restrict access, adhering to the Principle of Least Privilege.

### Example JSON Structure
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:ListBucket", "s3:GetObject"],
      "Resource": ["arn:aws:s3:::example-bucket/*"]
    }
  ]
}
```

- Create via AWS Console → IAM → Policies → Create policy.
- This example allows listing and getting objects from a specific S3 bucket.

## 7. Switching IAM Roles (from Lesson 3)

Switch Role allows users to assume another IAM role temporarily without logging out, enabling secure access across AWS accounts or environments.

### Steps
- AWS Console → [Your username in top-right] → Switch Role → Enter Account ID and Role Name → Switch.

### Benefits
- Secure access to multiple accounts (e.g., dev and prod).
- Avoids sharing passwords or long-term credentials.
- Provides granular access control and auditability.

## 8. Permissions Boundary (from Lesson 3)

A Permissions Boundary is an advanced IAM feature that sets the maximum scope of permissions an IAM entity (user or role) can have, acting as a guardrail.

### Use Cases
- Delegate administration safely without full root access.
- Limit permissions for junior admins or service roles.
- Prevent privilege escalation by capping allowable policies.

Attach via IAM → Users/Roles → Permissions boundary → Select policy.

## 9. Tracking Activities with AWS CloudTrail (from Lesson 3)

AWS CloudTrail records all user activity, API calls, and account changes in an AWS account for auditing and compliance.

### Capabilities
- Tracks who performed an action, when, and from where (e.g., IP address).
- Provides detailed audit trails stored in S3 buckets.
- Integrates with CloudWatch for real-time alerts on suspicious activity.
- View logs in CloudTrail Console or query via Athena.

Enable: AWS Console → CloudTrail → Create trail.

## 10. Policy Simulator Purpose

The IAM Policy Simulator is a tool to test and debug IAM policies without impacting real AWS resources.

### Functions
- Simulates API requests to verify if actions are allowed or denied.
- Supports testing multiple policies, roles, and resources.
- Useful for troubleshooting complex permission sets or verifying least privilege compliance.

Access: AWS Console → IAM → Policy Simulator.

## Control Questions

### 1. What is the essence of TOTP authentication? Give examples.
TOTP (Time-based One-Time Password) generates a unique, short-lived code (typically every 30 seconds) based on a shared secret key, synchronized between a server and an authenticator app. It enhances security by requiring a time-sensitive factor.

Examples: Google Authenticator, Microsoft Authenticator, Authy, AWS Virtual MFA.

### 2. Describe the JSON format: where it is used and its features. Does AWS use it?
JSON (JavaScript Object Notation) is a lightweight, text-based data interchange format that's easy for humans to read and machines to parse.

Features:
- Structured as key-value pairs, arrays, and objects.
- Language-independent and supported by most programming languages.
- Compact and human-readable.

Usage in AWS: Yes, extensively—for IAM policies, CloudFormation templates, Lambda function configurations, and API responses.

### 3. What types of Amazon APIs exist?
- **AWS Management Console API**: Web-based interface for graphical access to services.
- **AWS SDKs**: Language-specific libraries (e.g., Boto3 for Python, AWS SDK for Java, JavaScript).
- **AWS CLI**: Command-line interface for scripting and automation.
- **AWS REST APIs**: HTTP-based endpoints for direct programmatic integration (e.g., via tools like Postman).

### 4. How can AWS CLI be installed on different operating systems?
- **Windows**:
  ```
  msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
  ```
- **Linux**:
  ```
  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
  unzip awscliv2.zip
  sudo ./aws/install
  ```
- **macOS**:
  ```
  curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
  sudo installer -pkg AWSCLIV2.pkg -target /
  ```

### 5. Basic AWS CLI Commands (with examples)
- `aws configure`: Set up credentials and default region.
  ```
  aws configure
  ```
- `aws s3 ls`: List S3 buckets.
  ```
  aws s3 ls
  ```
- `aws ec2 describe-instances`: Describe EC2 instances.
  ```
  aws ec2 describe-instances
  ```
- `aws iam list-users`: List IAM users.
  ```
  aws iam list-users
  ```
- `aws s3 cp file.txt s3://mybucket/`: Upload a file to S3.
  ```
  aws s3 cp file.txt s3://mybucket/
  ```
- `aws cloudwatch describe-alarms`: View CloudWatch alarms.
  ```
  aws cloudwatch describe-alarms
  ```

## Conclusions

AWS provides a global, scalable, and cost-effective cloud platform offering compute, storage, networking, database, and security services. Through the use of IAM policies, MFA, and permissions boundaries, users can ensure secure access control following the principle of least privilege. Tools like Amazon Budgets and CloudTrail support effective cost management and activity monitoring, while JSON-based policies enable flexible and precise permission settings. Understanding TOTP authentication, IAM role switching, and AWS CLI usage allows for secure and automated cloud management. Overall, mastering these fundamental AWS concepts helps users efficiently operate in the cloud while maintaining high standards of security, reliability, and cost optimization.

---
