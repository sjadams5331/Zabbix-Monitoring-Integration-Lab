# Zabbix Monitoring Integration – Enterprise IT Operations Lab

## Overview

This project extends an existing enterprise-style IT home lab by integrating **Zabbix** as a centralized monitoring and alerting platform. The goal of this phase was to introduce proactive infrastructure monitoring that complements the existing **Active Directory** and **osTicket** environment, transforming the lab from a reactive helpdesk simulation into a full **IT operations and NOC-style workflow**.

Zabbix was deployed on a dedicated Ubuntu Server VM and configured to monitor both the Active Directory domain controller and the osTicket application server. This design mirrors real-world enterprise environments where monitoring systems provide early detection of issues before they impact users.

## Architecture Summary

### Core Components

- **Zabbix Server**
  - OS: Ubuntu Server
  - Role: Centralized monitoring and alerting platform
  - Network: Dual-homed (NAT + Host-only)
- **Active Directory Server**
  - OS: Windows Server
  - Role: Identity, authentication, DNS
- **osTicket Server**
  - OS: Debian Linux
  - Role: Internal IT helpdesk application
  - Authentication: LDAPS integrated with Active Directory

### Network Design

- **NAT Adapter**
  - Provides internet access for updates and package installation
- **Host-only Adapter (vboxnet0)**
  - Internal lab network
  - Enables secure, isolated communication between AD, osTicket, and Zabbix
  - Static IP addressing used for infrastructure consistency

This separation reflects enterprise best practices by isolating internal service communication from external network access.

## Monitoring Strategy

Zabbix was intentionally positioned as a **NOC-level monitoring layer** above existing infrastructure, rather than as a standalone tool.

### Active Directory Monitoring

The domain controller was monitored first due to its role as foundational infrastructure.

Monitored elements include:
- Host availability
- CPU, memory, and disk utilization
- LDAP/LDAPS service availability
- Core Windows services (AD DS, DNS)

**Rationale:**  
Active Directory outages impact authentication, authorization, and downstream applications. Monitoring AD provides early detection of issues that would otherwise surface later as application or user failures.

### osTicket Monitoring

The osTicket server was monitored as a business-critical internal application.

Monitored elements include:
- Host availability
- Web service availability (Apache/Nginx)
- Database service availability (MySQL/MariaDB)
- Disk usage related to ticket database growth
- Network connectivity to Active Directory over LDAPS

**Rationale:**  
Monitoring osTicket provides visibility into application-layer health and allows correlation between infrastructure issues (e.g., AD outages) and user-facing service impact.

## Dependency Awareness

A key design goal was modeling **cause-and-effect relationships** between systems:

- Active Directory failure → Authentication failures
- Authentication failures → osTicket login issues
- Zabbix detects AD issues before users submit tickets

This layered visibility reflects real enterprise operations, where monitoring systems are used to identify root causes rather than just symptoms.

## Alerting Philosophy

Alerting was designed to be **minimal, actionable, and realistic**, avoiding excessive noise.

Examples of alert conditions:
- Active Directory unreachable
- LDAP/LDAPS service unavailable
- osTicket web service down
- Disk utilization exceeding defined thresholds

Alerts were scoped to events that would require operator intervention in a real environment.

## Incident Simulation and Validation

To validate the monitoring setup, controlled service disruptions were performed (e.g., stopping critical services or simulating resource exhaustion). Zabbix successfully detected these events and generated alerts, confirming:

- Agent communication was functioning correctly
- Service checks were accurate
- Dependencies behaved as expected

This confirmed that the monitoring configuration provided meaningful operational visibility.

## Security Considerations

- LDAPS was used for secure authentication between osTicket and Active Directory
- Zabbix agents were configured using least-privilege principles
- Database access was restricted to a dedicated Zabbix database user
- Monitoring traffic was isolated within the host-only lab network

These measures align with common enterprise security practices.

## Outcome

This phase completed the transition from a reactive helpdesk-focused lab to a **proactive IT operations environment**. The integration of Zabbix demonstrates:

- Centralized infrastructure monitoring
- Cross-platform visibility (Windows and Linux)
- Awareness of system dependencies
- Realistic operational workflows

The lab now accurately reflects how monitoring, identity services, and ticketing systems interact in real-world enterprise IT environments.

## Project Status

This project phase is considered **complete** and intentionally frozen. Future work will focus on separate, standalone labs or certification study rather than continued expansion of this environment.

The environment remains available as a reference architecture and demonstration platform.
