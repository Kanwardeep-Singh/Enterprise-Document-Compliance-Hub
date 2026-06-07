# Role-Based Access Control (RBAC)

## Overview

The Enterprise Document Compliance Hub implements a Role-Based Access Control (RBAC) model to ensure that users can only access functionality and data required for their responsibilities.

The RBAC model aligns security controls with business roles, governance policies, and compliance requirements while supporting scalability across departments and business units.

The design follows the Principle of Least Privilege and Separation of Duties to minimize security risks and prevent unauthorized activities.

---

# Security Principles

The RBAC implementation is based on the following principles:

### Least Privilege

Users receive only the permissions necessary to perform their assigned tasks.

### Separation of Duties

Critical governance activities are distributed across multiple roles to reduce operational and compliance risk.

### Role-Based Authorization

Access is determined by business role rather than individual user configuration.

### Centralized Identity Management

All permissions are managed through Microsoft Entra ID security groups.

---

# Authorization Architecture

```text
Microsoft Entra ID
         │
         ▼
Security Groups
         │
         ▼
Power Apps
         │
         ▼
Power Automate
         │
         ▼
SharePoint Online
```

Authorization decisions are consistently enforced across all application layers.

---

# Role Definitions

## Viewer

### Description

Standard users who consume controlled documents.

### Permissions

* View documents
* Search repository
* Access PDF viewer
* View metadata

### Restrictions

* Cannot modify documents
* Cannot approve reviews
* Cannot access administration functions

---

## Reviewer

### Description

Responsible for conducting document reviews and validating compliance requirements.

### Permissions

* All Viewer permissions
* Submit reviews
* Add review comments
* Update review outcomes

### Restrictions

* Cannot perform administrative actions
* Cannot modify governance settings

---

## Compliance Manager

### Description

Responsible for monitoring compliance activities and managing review processes.

### Permissions

* Review oversight
* Approval actions
* Compliance reporting
* Ownership assignment

### Restrictions

* Limited configuration access

---

## Administrator

### Description

Platform owners responsible for governance and operational management.

### Permissions

* Full application access
* User management
* Security administration
* Governance configuration
* Environment maintenance

---

# Permission Matrix

| Capability                 | Viewer | Reviewer | Manager | Administrator |
| -------------------------- | ------ | -------- | ------- | ------------- |
| View Documents             | ✓      | ✓        | ✓       | ✓             |
| Search Repository          | ✓      | ✓        | ✓       | ✓             |
| View PDF                   | ✓      | ✓        | ✓       | ✓             |
| Submit Reviews             | ✗      | ✓        | ✓       | ✓             |
| Approve Documents          | ✗      | ✗        | ✓       | ✓             |
| Manage Users               | ✗      | ✗        | ✗       | ✓             |
| Configure Governance       | ✗      | ✗        | ✗       | ✓             |
| Environment Administration | ✗      | ✗        | ✗       | ✓             |

---

# Power Apps Security Enforcement

Role information is evaluated at runtime.

Examples include:

### Screen Visibility

Administrative screens remain inaccessible to non-administrative users.

### Navigation Controls

Menu items are dynamically rendered based on assigned roles.

### Action Availability

Review and approval actions are displayed only when appropriate permissions exist.

---

# SharePoint Security

Document repositories inherit security controls from:

* SharePoint Permission Groups
* Site Collection Permissions
* Library Permissions
* Item-Level Security

This ensures governance controls remain enforced regardless of application access.

---

# Workflow Security

Power Automate workflows validate:

* User permissions
* Status transitions
* Approval authority
* Governance requirements

Unauthorized workflow actions are automatically blocked.

---

# Audit & Monitoring

RBAC activities are monitored through:

* User access logs
* SharePoint audit history
* Workflow execution history
* Administrative activity records

---

# Governance Benefits

The RBAC model delivers:

* Reduced security risk
* Improved compliance posture
* Consistent authorization controls
* Enhanced auditability
* Scalable permission management

The resulting security framework supports enterprise-grade governance and aligns with modern identity-centric security principles.
