# 🔗 Federated Identity Management

## File Structure

```
lesson-07-aws-access-management/
└── 06-federated-identity-management/
```
- [readme.md](./readme.md)
- [diagram.drawio](./diagram.drawio)
- [diagram.png](./diagram.png)

## Introduction

Federation allows users to access AWS resources using existing identities from external identity providers (IdPs) without creating separate IAM users. This enables organizations to use their existing corporate directories and identity systems to control access to AWS.

## What is Federation?

Federation is a system where users authenticate with an external identity provider, and that authentication is trusted by AWS to grant access to AWS resources.

```
+------------------------------------------------------------------+
|                    IDENTITY FEDERATION                            |
+------------------------------------------------------------------+
|                                                                   |
|   User ---> Corporate IdP ---> AWS STS ---> AWS Resources         |
|                                                                   |
|   1. User logs into      2. IdP sends        3. User accesses     |
|      corporate system       assertion to AWS     AWS with temp    |
|                                                  credentials      |
+------------------------------------------------------------------+
```

## Why Use Federation?

| Benefit | Description |
|---------|-------------|
| Single identity | Users use existing corporate credentials |
| Centralized management | Manage users in one place |
| No IAM users needed | Don't create separate AWS users |
| Automatic provisioning | Users get access when joining company |
| Automatic deprovisioning | Access removed when leaving company |
| Compliance | Meet audit requirements |

## Federation Types

### SAML 2.0 Federation

Security Assertion Markup Language - industry standard for SSO.

| Feature | Description |
|---------|-------------|
| Protocol | SAML 2.0 |
| Use case | Enterprise SSO |
| IdPs | ADFS, Okta, Ping, OneLogin |
| Integration | IAM Identity Center, IAM |

### Web Identity Federation

For mobile and web applications using social identity providers.

| Feature | Description |
|---------|-------------|
| Protocol | OAuth 2.0 / OpenID Connect |
| Use case | Mobile apps, web apps |
| IdPs | Amazon, Google, Facebook, Apple |
| Service | Amazon Cognito (recommended) |

### Custom Identity Broker

For organizations with custom authentication systems.

| Feature | Description |
|---------|-------------|
| Use case | Custom authentication systems |
| Method | Application calls STS directly |
| Complexity | Higher implementation effort |

## SAML 2.0 Federation Flow

```
+------------------------------------------------------------------+
|                    SAML FEDERATION FLOW                           |
+------------------------------------------------------------------+
|                                                                   |
|   1. User accesses        2. Redirected to IdP                    |
|      AWS resource            for authentication                   |
|   +-----------+           +-----------+                           |
|   |   User    | --------> |    IdP    |                           |
|   +-----------+           +-----------+                           |
|                                 |                                 |
|   4. Access AWS           3. SAML assertion                       |
|      with temp creds         sent to AWS                          |
|   +-----------+           +-----------+                           |
|   |    AWS    | <-------- |  AWS STS  |                           |
|   +-----------+           +-----------+                           |
|                                                                   |
+------------------------------------------------------------------+
```

### SAML Federation Steps

| Step | Action |
|------|--------|
| 1 | User attempts to access AWS |
| 2 | User redirected to corporate IdP |
| 3 | User authenticates with corporate credentials |
| 4 | IdP generates SAML assertion |
| 5 | SAML assertion sent to AWS STS |
| 6 | STS validates assertion and returns temporary credentials |
| 7 | User accesses AWS with temporary credentials |

## Amazon Cognito

Recommended for web and mobile identity federation.

### Cognito Features

| Feature | Description |
|---------|-------------|
| User Pools | User directory with sign-up/sign-in |
| Identity Pools | Federated identities for AWS access |
| Social sign-in | Google, Facebook, Amazon, Apple |
| Enterprise | SAML, OIDC providers |
| Customizable | Branded UI, custom workflows |

### Cognito Identity Pools

```
+------------------------------------------------------------------+
|                    COGNITO IDENTITY POOLS                         |
+------------------------------------------------------------------+
|                                                                   |
|   +------------+  +------------+  +------------+                  |
|   |  Google    |  |  Facebook  |  |   SAML     |                  |
|   +------------+  +------------+  +------------+                  |
|         |              |               |                          |
|         +-------+------+-------+-------+                          |
|                 |                                                 |
|                 v                                                 |
|         +----------------+                                        |
|         | Cognito        |                                        |
|         | Identity Pool  |                                        |
|         +----------------+                                        |
|                 |                                                 |
|                 v                                                 |
|         +----------------+                                        |
|         | Temporary AWS  |                                        |
|         | Credentials    |                                        |
|         +----------------+                                        |
|                                                                   |
+------------------------------------------------------------------+
```

## Federation Comparison

| Federation Type | Use Case | Complexity | Recommended For |
|-----------------|----------|------------|-----------------|
| IAM Identity Center | Workforce access | Low | Multi-account |
| SAML 2.0 Direct | Enterprise SSO | Medium | Single account |
| Cognito | Web/Mobile apps | Low | Consumer apps |
| Web Identity | Social login | Medium | Consumer apps |
| Custom Broker | Custom auth | High | Special cases |

## AWS Services for Federation

| Service | Purpose |
|---------|---------|
| IAM Identity Center | Workforce SSO |
| Amazon Cognito | Web/mobile identity |
| AWS STS | Temporary credentials |
| IAM Roles | Define federated access |

## Federation Best Practices

1. **Use IAM Identity Center** for workforce access
2. **Use Cognito** for customer-facing applications
3. **Define appropriate IAM roles** for federated users
4. **Use least privilege** for federated roles
5. **Set appropriate session duration** for temporary credentials
6. **Monitor federated access** with CloudTrail

## 🎯 Exam Tips

- **Federation** = external users accessing AWS
- **SAML 2.0** = enterprise federation standard
- **Cognito** = recommended for web/mobile apps
- **No IAM users created** for federated users
- **Temporary credentials** from AWS STS
- Know that **IAM Identity Center** uses federation
- **Web identity federation** = social logins (Google, Facebook)

## 🔑 Key Terms

| Term | Definition |
|------|------------|
| Federation | Trust relationship with external IdP |
| IdP | Identity Provider (external auth system) |
| SAML | Security Assertion Markup Language |
| Cognito | AWS service for web/mobile identity |
| STS | Security Token Service |
| Assertion | Authentication statement from IdP |
| OIDC | OpenID Connect |

## 💡 Key Takeaways

1. Federation allows external users to access AWS without IAM users
2. SAML 2.0 is the standard for enterprise federation
3. Amazon Cognito is recommended for web and mobile applications
4. Federated users receive temporary credentials from STS
5. IAM Identity Center provides the simplest federation for workforce access
6. Federation enables centralized identity management

---

*Next: [07 - Cross-Account Access](../07-cross-account-access/readme.md)*
