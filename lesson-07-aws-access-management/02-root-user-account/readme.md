# 👤 AWS Root User Account

## File Structure

```
lesson-07-aws-access-management/
└── 02-root-user-account/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

The AWS root user is the identity that has complete access to all AWS services and resources in an account. Understanding how to secure and when to use the root user is critical for AWS security and is frequently tested on the Cloud Practitioner exam.

## What is the Root User?

The root user is created when you first create an AWS account. It has unrestricted access to all resources in the account and cannot be limited by IAM policies.

```
+------------------------------------------------------------------+
|                    AWS ROOT USER                                  |
+------------------------------------------------------------------+
|                                                                   |
|    +------------------+                                           |
|    |   ROOT USER      |    FULL ACCESS TO EVERYTHING              |
|    |   (email + pw)   |    Cannot be restricted                   |
|    +------------------+                                           |
|            |                                                      |
|            | Unrestricted Access                                  |
|            v                                                      |
|    +--------------------------------------------------+          |
|    |              ALL AWS SERVICES                    |          |
|    |  +--------+ +--------+ +--------+ +--------+     |          |
|    |  |  IAM   | |  EC2   | |   S3   | | Billing|     |          |
|    |  +--------+ +--------+ +--------+ +--------+     |          |
|    |  +--------+ +--------+ +--------+ +--------+     |          |
|    |  |  RDS   | | Lambda | |  VPC   | | Account|     |          |
|    |  +--------+ +--------+ +--------+ +--------+     |          |
|    +--------------------------------------------------+          |
|                                                                   |
+------------------------------------------------------------------+
```

## Root User Credentials

| Credential | Description | Use |
|------------|-------------|-----|
| Email address | Account identifier | Sign-in to console |
| Password | Authentication | Sign-in to console |
| Access keys | API/CLI access | Should NOT be created |
| MFA device | Second factor | MUST be enabled |

## Tasks That Require Root User

Only the root user can perform certain tasks:

| Task | Description |
|------|-------------|
| Change account settings | Account name, email, root password |
| Close AWS account | Permanently close the account |
| Restore IAM permissions | When IAM admin locked themselves out |
| Change AWS Support plan | Upgrade/downgrade support level |
| Register as seller in Marketplace | Become an AWS Marketplace seller |
| Configure S3 bucket for MFA Delete | Enable MFA delete on S3 |
| Edit/Delete S3 bucket policy with invalid VPC ID | Fix broken bucket policies |
| Sign up for GovCloud | Access AWS GovCloud regions |
| Enable MFA Delete on S3 | Require MFA for object deletion |
| View certain tax invoices | Access specific billing documents |

## Root User Security Best Practices

### Must Do

| Best Practice | Why |
|---------------|-----|
| Enable MFA | Add second authentication factor |
| Use strong password | Prevent unauthorized access |
| Don't use for daily tasks | Reduce risk of compromise |
| Don't create access keys | Prevent programmatic access |
| Store credentials securely | Protect login information |

### Should Do

| Best Practice | Why |
|---------------|-----|
| Create IAM admin user | Use for day-to-day admin tasks |
| Set up billing alerts | Monitor account usage |
| Enable CloudTrail | Audit root user activity |
| Use account contacts | Set alternate contacts for security |

## Root User vs IAM Admin User

```
+------------------------------------------------------------------+
|              ROOT USER vs IAM ADMIN USER                          |
+------------------------------------------------------------------+
|                                                                   |
|  +---------------------------+  +---------------------------+     |
|  |       ROOT USER           |  |    IAM ADMIN USER         |     |
|  +---------------------------+  +---------------------------+     |
|  | • Unrestricted access     |  | • Policy-based access     |     |
|  | • Cannot be limited       |  | • Can be limited          |     |
|  | • Account-level tasks     |  | • Day-to-day operations   |     |
|  | • Billing management      |  | • Resource management     |     |
|  | • USE RARELY              |  | • USE DAILY               |     |
|  +---------------------------+  +---------------------------+     |
|                                                                   |
|  Best Practice: Create IAM admin, lock away root credentials      |
|                                                                   |
+------------------------------------------------------------------+
```

| Feature | Root User | IAM Admin |
|---------|-----------|-----------|
| Access level | Unrestricted | Policy-defined |
| Can be deleted | No | Yes |
| Can be limited | No | Yes |
| MFA requirement | Should enable | Should enable |
| Access keys | Should NOT create | Can create (not recommended) |
| Daily use | NO | YES |

## Setting Up Root User Security

### Step 1: Enable MFA

Types of MFA devices:

| MFA Type | Description |
|----------|-------------|
| Virtual MFA | App on smartphone (Authy, Google Auth) |
| Hardware MFA | Physical key fob |
| FIDO2 security key | YubiKey, other FIDO devices |

### Step 2: Create IAM Admin User

```
1. Sign in as root user
2. Create IAM user with AdministratorAccess policy
3. Enable MFA on IAM admin user
4. Sign out of root account
5. Use IAM admin for daily tasks
6. Store root credentials securely
```

### Step 3: Secure Root Credentials

| Action | Description |
|--------|-------------|
| Remove access keys | Delete any root access keys |
| Store password securely | Use password manager or secure vault |
| Document MFA recovery | Store MFA recovery information |
| Set alternate contacts | Security, billing, operations contacts |

## Root User Access Alerts

Set up alerts for root user activity:

| Alert Type | Service | Purpose |
|------------|---------|---------|
| Console sign-in | CloudWatch Events | Detect root login |
| API calls | CloudTrail + CloudWatch | Monitor root actions |
| Billing alerts | AWS Budgets | Track spending |

## 🎯 Exam Tips

- Root user has **unrestricted access** - cannot be limited
- **Enable MFA** on root user immediately
- **Don't create access keys** for root user
- **Don't use root for daily tasks** - create IAM admin instead
- Know the **tasks that require root user** (close account, change support plan, etc.)
- Root user credentials = **email address + password**
- Root user is the **only identity** that can close an AWS account

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Root User | Account owner with unrestricted access |
| MFA | Multi-Factor Authentication |
| Virtual MFA | Software-based authentication app |
| Hardware MFA | Physical authentication device |
| Access Keys | Credentials for programmatic AWS access |
| Account Settings | Configuration only root can change |

## 💡 Key Takeaways

1. Root user has complete, unrestricted access to the AWS account
2. Enable MFA on root user immediately after account creation
3. Never create access keys for the root user
4. Use IAM admin user for daily administrative tasks
5. Only use root user for tasks that specifically require it
6. Store root credentials securely and limit access to them

---

*Next: [03 - Principle of Least Privilege](../03-principle-of-least-privilege/readme.md)*
