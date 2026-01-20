# osTicket Helpdesk Home Lab – Enterprise Service Desk Simulation

## Overview

This project implements a fully functional **osTicket-based helpdesk platform** designed to simulate a real-world enterprise IT service desk. The environment integrates tightly with **Microsoft Active Directory** using secure LDAPS authentication and demonstrates realistic service desk operations, including role-based access control, SLA enforcement, escalation workflows, and tiered support structures.

The lab is designed to reflect how a small-to-mid-size organization might deploy and operate a production helpdesk system. Emphasis is placed on operational realism, security, and documentation quality rather than basic application installation.

## Environment Summary

- **Hypervisor:** Oracle VirtualBox  
- **Operating System:** Debian GNU/Linux 12 (Bookworm)  
- **Web Server:** Apache 2  
- **Application Stack:** PHP 8.2  
- **Database:** MariaDB  
- **Helpdesk Platform:** osTicket v1.18.x  
- **Directory Services:** Microsoft Active Directory  
- **Authentication Method:** LDAP over SSL (LDAPS)

## Architecture and Design

The deployment follows a **centralized application server model**, commonly used in enterprise internal support environments.

### Architecture Components

- Dedicated Debian Linux VM hosting osTicket
- Apache serving the web frontend
- PHP handling application logic
- MariaDB providing persistent data storage
- Windows Server acting as the Active Directory domain controller
- Secure LDAPS communication between osTicket and Active Directory

This architecture prioritizes clarity, maintainability, and enterprise-aligned security practices while remaining realistic for a lab environment.

## Authentication and Identity Integration

osTicket is fully integrated with Active Directory using **LDAP over SSL (LDAPS)** to ensure secure, centralized authentication and identity consistency.

### Active Directory Configuration

- **Domain:** lab.local  
- **Domain Controller:** dc01.lab.local  
- **LDAPS Port:** 636  
- **Service Account:** svc_osticket@lab.local  

The Debian server trusts the internal Microsoft Certificate Authority, allowing encrypted and validated directory communication.

### Authentication Model

- End users authenticate using Active Directory credentials
- Support agents authenticate using Active Directory accounts
- A dedicated service account performs directory queries
- Directory access is restricted to read-only permissions
- All authentication traffic is encrypted using TLS

## Role-Based Access Control (RBAC)

Access within osTicket is enforced using departments, roles, and permission sets that reflect enterprise service desk separation of duties.

### Defined Support Roles

- **Tier 1 Support**
  - User-facing ticket handling
  - Basic troubleshooting and issue resolution
- **Tier 2 Support**
  - Escalated issue handling
  - Ticket reassignment and priority adjustment
- **NOC / Infrastructure**
  - Infrastructure-focused ticket visibility
  - Limited exposure to end-user data
- **Administrator**
  - Full system configuration and management access

Roles are mapped to departments and designed to mirror real-world service desk team structures.

## Helpdesk Workflows

### Ticket Intake

- Web-based user portal authenticated via Active Directory
- Categorized help topics aligned with enterprise service catalogs
- Automatic routing based on department and issue type

### Ticket Lifecycle

1. Ticket submission by authenticated user  
2. Automatic categorization and routing  
3. Agent assignment  
4. User communication and internal documentation  
5. Escalation or reassignment when required  
6. Issue resolution and closure  
7. Post-resolution handling and SLA evaluation  

### Service Level Agreements (SLAs)

- Priority-based SLAs (P1–P3)
- Defined response and resolution targets
- SLA enforcement based on ticket category and department

## Security Considerations

### Application Security

- Role-based permission enforcement
- Separation of user, agent, and administrative interfaces
- Removal of installation artifacts post-deployment

### Server Security

- Dedicated database user for osTicket
- Restricted file permissions and ownership
- Isolation between web server, database, and system services

### Directory Security

- Encrypted LDAPS communication
- Least-privilege service account usage
- Certificate-based trust validation

## Validation and Testing

The deployment was validated through controlled testing, including:

- Successful Active Directory–authenticated user logins
- Agent authentication with role-based permission enforcement
- Ticket creation, routing, escalation, and resolution
- SLA enforcement verification
- Service restarts without configuration loss
- Validation of secure LDAPS communication

## Troubleshooting and Lessons Learned

Issues encountered during deployment were resolved using standard enterprise troubleshooting techniques, including:

- Apache and PHP log analysis
- PHP extension dependency resolution
- Database authentication troubleshooting
- File permission and ownership correction
- Certificate trust validation for LDAPS

Reinstallation was intentionally avoided in favor of structured troubleshooting to better simulate real-world operational practices.

## Documentation Structure

Supporting documentation, configuration notes, and screenshots are maintained in the following directories:

- `/docs` – Detailed configuration and design documentation  
- `/screenshots` – Visual validation of key configurations and workflows  

## Skills Demonstrated

- Linux server administration (Debian)
- Web application deployment and hardening
- Apache and PHP configuration
- MariaDB administration
- Active Directory integration using LDAPS
- Role-based access control design
- Enterprise service desk workflow implementation
- SLA design and enforcement
- Log analysis and structured troubleshooting
- Enterprise-grade technical documentation

## Project Status

This project phase is considered **complete** and intentionally frozen. The environment serves as a reference implementation for enterprise service desk operations and is designed to integrate with additional infrastructure components such as centralized monitoring and NOC workflows.
