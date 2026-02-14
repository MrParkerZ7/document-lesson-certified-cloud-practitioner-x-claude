# 🔑 AWS Authentication Methods

## File Structure

```
lesson-07-aws-access-management/
└── 04-authentication-methods/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Authentication is the process of verifying identity - confirming that someone is who they claim to be. AWS provides multiple authentication methods to secure access to AWS resources through the console, CLI, and API.

## Authentication vs Authorization

| Concept | Question | AWS Service |
|---------|----------|-------------|
| Authentication | Who are you? | IAM credentials, MFA |
| Authorization | What can you do? | IAM policies |

```
+------------------------------------------------------------------+
|            AUTHENTICATION vs AUTHORIZATION                        |
+------------------------------------------------------------------+
|                                                                   |
|   AUTHENTICATION                AUTHORIZATION                     |
|   (Identity)                    (Permissions)                     |
|                                                                   |
|   +----------------+            +----------------+                 |
|   | Username       |            | IAM Policies   |                 |
|   | Password       |    --->    | Can access S3? |                 |
|   | MFA Token      |            | Can launch EC2?|                 |
|   +----------------+            +----------------+                 |
|                                                                   |
|   "Prove you are John"          "John can read S3 bucket X"       |
|                                                                   |
+------------------------------------------------------------------+
```

## AWS Authentication Methods

### 1. Username and Password

Used for AWS Management Console access.

| Feature | Description |
|---------|-------------|
| Use case | Human users accessing console |
| Requirements | IAM user account |
| Security | Should combine with MFA |
| Password policy | Customizable requirements |

### 2. Access Keys

Used for programmatic access (CLI, SDK, API).

| Component | Description |
|-----------|-------------|
| Access Key ID | Public identifier (like username) |
| Secret Access Key | Secret (like password) - shown only once |

**Best Practices:**
- Never share access keys
- Rotate keys regularly
- Never commit to source code
- Use IAM roles instead when possible

### 3. Multi-Factor Authentication (MFA)

Adds a second layer of authentication.

| MFA Type | Description | Example |
|----------|-------------|---------|
| Virtual MFA | Software app | Authy, Google Authenticator |
| Hardware MFA | Physical device | Gemalto key fob |
| FIDO2 Security Key | USB device | YubiKey |

### 4. Temporary Security Credentials

Provided by AWS Security Token Service (STS).

| Feature | Description |
|---------|-------------|
| Duration | Short-lived (minutes to hours) |
| Source | IAM roles, federation |
| Components | Access key, secret key, session token |
| Use case | Cross-account, federation, EC2 roles |

## Authentication by Access Method

### Console Access

```
+------------------------------------------------------------------+
|                    CONSOLE AUTHENTICATION                         |
+------------------------------------------------------------------+
|                                                                   |
|   User ---> Account ID + Username + Password ---> AWS Console     |
|                      +                                            |
|                 MFA Token (recommended)                           |
|                                                                   |
+------------------------------------------------------------------+
```

### CLI/SDK Access

```
+------------------------------------------------------------------+
|                    CLI/SDK AUTHENTICATION                         |
+------------------------------------------------------------------+
|                                                                   |
|   Developer ---> Access Key ID + Secret Access Key ---> AWS API   |
|                                                                   |
|   OR                                                              |
|                                                                   |
|   EC2 Instance ---> IAM Role (auto credentials) ---> AWS API      |
|                                                                   |
+------------------------------------------------------------------+
```

## Password Policy

AWS allows customization of password requirements:

| Setting | Options |
|---------|---------|
| Minimum length | 6-128 characters |
| Character requirements | Upper, lower, numbers, symbols |
| Expiration | Days until password must be changed |
| Prevent reuse | Number of previous passwords blocked |
| Self-service | Allow users to change own password |

## MFA Enforcement

| Level | Implementation |
|-------|----------------|
| User level | Enable MFA per user |
| Policy level | Deny actions without MFA |
| Organization level | SCP requiring MFA |

### MFA Condition in Policy

```json
{
    "Condition": {
        "Bool": {
            "aws:MultiFactorAuthPresent": "true"
        }
    }
}
```

## AWS Security Token Service (STS)

STS provides temporary credentials for:

| Use Case | STS Action |
|----------|------------|
| Assume a role | AssumeRole |
| Cross-account access | AssumeRole |
| SAML federation | AssumeRoleWithSAML |
| Web identity | AssumeRoleWithWebIdentity |
| Temporary IAM user | GetSessionToken |

## Authentication Flow Examples

### Example 1: Console Sign-in with MFA

```
1. User enters account ID / alias
2. User enters username and password
3. User enters MFA code from device
4. AWS validates all credentials
5. User granted console access
```

### Example 2: EC2 Instance Accessing S3

```
1. Application runs on EC2 instance
2. Instance has IAM role attached
3. AWS automatically provides credentials
4. Application uses credentials to access S3
5. No access keys stored in code!
```

## 🎯 Exam Tips

- Know the difference between **authentication** and **authorization**
- **Password** = console access; **Access keys** = programmatic access
- **MFA** adds second authentication factor
- **Never embed access keys** in code
- Use **IAM roles** for EC2 and Lambda (no access keys needed)
- **STS** provides temporary credentials
- **Access Key ID** is public; **Secret Access Key** is private

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Authentication | Verifying identity |
| Authorization | Determining permissions |
| Access Key ID | Public part of access key |
| Secret Access Key | Private part of access key |
| MFA | Multi-Factor Authentication |
| STS | Security Token Service |
| Session Token | Part of temporary credentials |

## 💡 Key Takeaways

1. Authentication verifies identity; authorization determines permissions
2. Console uses username/password; CLI/API uses access keys
3. MFA adds critical security layer - enable on all users
4. Never store access keys in code - use IAM roles
5. Temporary credentials from STS are more secure than long-term keys
6. EC2 instances should use IAM roles, not access keys

---

*Next: [05 - AWS IAM Identity Center](../05-aws-iam-identity-center/readme.md)*
