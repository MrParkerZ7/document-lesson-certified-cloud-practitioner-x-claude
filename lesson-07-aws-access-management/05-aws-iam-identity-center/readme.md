# 🔐 AWS IAM Identity Center

## File Structure

```
lesson-07-aws-access-management/
└── 05-aws-iam-identity-center/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

AWS IAM Identity Center (formerly AWS Single Sign-On or AWS SSO) is the recommended service for managing workforce access to multiple AWS accounts and business applications. It provides a single place to create or connect workforce identities and manage their access centrally.

## What is IAM Identity Center?

IAM Identity Center enables you to manage access to all your AWS accounts and cloud applications from a single location. Users sign in once and can access all their assigned accounts and applications without re-entering credentials.

```
+------------------------------------------------------------------+
|                    AWS IAM IDENTITY CENTER                        |
+------------------------------------------------------------------+
|                                                                   |
|                    +--------------------+                         |
|                    | Identity Source    |                         |
|                    | (Users & Groups)   |                         |
|                    +--------------------+                         |
|                             |                                     |
|                             v                                     |
|                    +--------------------+                         |
|                    | IAM Identity Center|                         |
|                    | (Central Hub)      |                         |
|                    +--------------------+                         |
|                             |                                     |
|              +--------------+--------------+                      |
|              |              |              |                       |
|              v              v              v                       |
|     +------------+  +------------+  +------------+                |
|     | AWS Acct 1 |  | AWS Acct 2 |  | Bus Apps   |                |
|     +------------+  +------------+  +------------+                |
|                                                                   |
+------------------------------------------------------------------+
```

## Key Features

| Feature | Description |
|---------|-------------|
| Single Sign-On | One login for all accounts and applications |
| Centralized access | Manage access from one place |
| Multi-account | Works with AWS Organizations |
| Application access | SAML 2.0 business applications |
| Built-in directory | Or connect to existing identity provider |
| Free service | No additional charge |

## Identity Sources

IAM Identity Center can use different identity sources:

| Source | Description | Best For |
|--------|-------------|----------|
| Identity Center Directory | Built-in user directory | Small organizations |
| Active Directory | AWS Managed AD or AD Connector | Windows environments |
| External IdP | Okta, Azure AD, etc. | Enterprise SSO |

### Identity Source Comparison

```
+------------------------------------------------------------------+
|                    IDENTITY SOURCES                               |
+------------------------------------------------------------------+
|                                                                   |
|  +------------------+  +------------------+  +------------------+ |
|  | Identity Center  |  |  Active Directory|  |  External IdP    | |
|  |    Directory     |  |                  |  |                  | |
|  +------------------+  +------------------+  +------------------+ |
|  | Built-in         |  | AWS Managed AD   |  | Okta             | |
|  | Create users     |  | AD Connector     |  | Azure AD         | |
|  | Simple setup     |  | Existing users   |  | Ping Identity    | |
|  | Small teams      |  | Windows env      |  | OneLogin         | |
|  +------------------+  +------------------+  +------------------+ |
|                                                                   |
+------------------------------------------------------------------+
```

## Permission Sets

Permission sets define what users can do in AWS accounts.

| Concept | Description |
|---------|-------------|
| Permission Set | Collection of policies assigned to users |
| AWS Managed | Pre-built by AWS (e.g., AdministratorAccess) |
| Custom | Policies you create |
| Session duration | How long credentials are valid |

### How Permission Sets Work

```
User/Group + Permission Set + AWS Account = Access
```

| Component | Example |
|-----------|---------|
| User | John Smith |
| Permission Set | DeveloperAccess |
| Account | Development Account |
| Result | John has developer permissions in dev account |

## User Portal

IAM Identity Center provides a user portal where users can:

- See all assigned AWS accounts
- Launch console sessions
- Access business applications
- View available roles
- Get CLI credentials

## Integration with AWS Organizations

| Feature | Benefit |
|---------|---------|
| Automatic account discovery | See all accounts in organization |
| Delegated administration | Assign admin to member accounts |
| Centralized management | Manage from management account |
| Consistent permissions | Apply same permission sets across accounts |

## Setting Up IAM Identity Center

### Step 1: Enable IAM Identity Center

```
1. Go to IAM Identity Center in AWS Console
2. Choose your identity source
3. Enable in your organization
```

### Step 2: Create Users or Connect IdP

| Option | Steps |
|--------|-------|
| Built-in directory | Create users and groups directly |
| Active Directory | Connect to your AD |
| External IdP | Configure SAML connection |

### Step 3: Create Permission Sets

| Type | Examples |
|------|----------|
| AWS Managed | AdministratorAccess, ViewOnlyAccess |
| Custom | Create with specific permissions |

### Step 4: Assign Access

```
Select User/Group -> Select Account(s) -> Select Permission Set(s)
```

## Benefits Over Traditional IAM

| Traditional IAM | IAM Identity Center |
|-----------------|---------------------|
| Separate users per account | Single user, multiple accounts |
| Individual passwords | Single sign-on |
| Manual access management | Centralized management |
| No built-in SSO | Built-in SSO portal |
| Complex cross-account | Simple multi-account access |

## 🎯 Exam Tips

- **IAM Identity Center** = recommended for workforce access
- Formerly called **AWS Single Sign-On (SSO)**
- Works with **AWS Organizations**
- **Free service**
- **Permission sets** define access to accounts
- Can use built-in directory or external identity provider
- Users access through **user portal**
- Provides **temporary credentials** (not long-term access keys)

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| IAM Identity Center | Centralized workforce identity management |
| Permission Set | Collection of policies for account access |
| Identity Source | Where users are defined (directory, IdP) |
| User Portal | Web interface for user access |
| SAML | Protocol for SSO with business applications |
| AWS Organizations | Multi-account management service |

## 💡 Key Takeaways

1. IAM Identity Center is the recommended way to manage workforce access
2. It enables single sign-on across all AWS accounts and applications
3. Works seamlessly with AWS Organizations
4. Can use built-in directory or connect to external identity providers
5. Permission sets define what users can do in accounts
6. Free service with no additional charges

---

*Next: [06 - Federated Identity Management](../06-federated-identity-management/readme.md)*
