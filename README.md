# Zabbix Monitoring Home Lab – Enterprise NOC Simulation

## Overview

This project implements a fully functional **Zabbix monitoring platform** designed to simulate how enterprise IT operations teams proactively monitor infrastructure and critical services. The deployment integrates with an existing lab environment consisting of **Active Directory** and an **osTicket helpdesk**, positioning Zabbix as a centralized NOC-style monitoring layer.

The lab emphasizes infrastructure visibility, dependency awareness, and operational realism. Rather than focusing solely on metric collection, the environment is designed to demonstrate how monitoring supports early detection, incident response, and service continuity in enterprise IT environments.

## Environment Summary

- **Hypervisor:** Oracle VirtualBox  
- **Operating System:** Ubuntu Server  
- **Monitoring Platform:** Zabbix Server 6.x  
- **Web Frontend:** Apache  
- **Database:** MariaDB  
- **Monitored Systems:**
  - Microsoft Active Directory (Windows Server)
  - osTicket Helpdesk (Debian Linux)

## Architecture and Design

The monitoring deployment follows a **centralized monitoring server model** commonly used in enterprise Network Operations Centers (NOCs).

### Architecture Components

- Dedicated Ubuntu Server VM hosting Zabbix Server and Web Frontend
- MariaDB providing persistent storage for monitoring data
- Zabbix agents installed on monitored hosts
- Windows Server domain controller monitored for identity and directory services
- Debian-based osTicket server monitored for application and database health

### Network Design

- **NAT Adapter**
  - Provides internet access for updates and package installation
- **Host-only Adapter**
  - Isolated internal lab network
  - Enables secure monitoring traffic between Zabbix, Active Directory, and osTicket
  - Static IP addressing used for infrastructure consistency

This dual-network approach mirrors enterprise designs that separate internal monitoring traffic from external network access.

## Monitoring Strategy

Zabbix was intentionally deployed as a **proactive monitoring layer**, positioned upstream of user-facing systems.

Monitoring priorities were defined based on infrastructure dependencies rather than application visibility alone.

## Active Directory Monitoring

Active Directory was monitored first due to its role as foundational infrastructure.

### Monitored Elements

- Host availability
- CPU, memory, and disk utilization
- LDAP and LDAPS service availability
- Core Windows services (Active Directory Domain Services, DNS)

### Rationale

Active Directory outages directly impact authentication, authorization, and downstream applications such as osTicket. Monitoring AD enables early detection of identity-related failures before they manifest as user-facing incidents.

## osTicket Monitoring

The osTicket helpdesk server was monitored as a business-critical internal application.

### Monitored Elements

- Host availability
- Web service availability (Apache)
- Database service availability (MariaDB)
- Disk utilization related to ticket database growth
- Network connectivity to Active Directory over LDAPS

### Rationale

Monitoring osTicket provides application-layer visibility and enables correlation between infrastructure failures and service desk impact.

## Dependency Awareness

The monitoring design explicitly models **cause-and-effect relationships** between systems:

- Active Directory degradation impacts authentication services
- Authentication failures affect osTicket access
- Zabbix detects infrastructure issues before users submit tickets

This dependency awareness reflects real-world enterprise monitoring practices focused on root cause identification rather than symptom tracking.

## Alerting Philosophy

Alerting was designed to be **minimal, actionable, and realistic**, avoiding unnecessary noise.

### Example Alert Conditions

- Active Directory host unreachable
- LDAP/LDAPS service unavailable
- osTicket web service down
- Disk utilization exceeding defined thresholds

Alerts were scoped to events that would require operator intervention in a production environment.

## Validation and Testing

The monitoring configuration was validated through controlled testing, including:

- Verification of agent communication on all monitored hosts
- Detection of stopped services on monitored systems
- Confirmation of alert generation for critical failures
- Restoration of services and verification of recovery detection

Testing confirmed that Zabbix provided accurate, timely visibility into both infrastructure and application health.

## Security Considerations

### Monitoring Security

- Zabbix agents configured with least-privilege access
- Monitoring traffic isolated within the host-only lab network
- Database access restricted to a dedicated Zabbix database user

### Network Security

- Internal monitoring traffic separated from external access
- Static IP addressing for core infrastructure systems
- No direct exposure of monitoring services to external networks

## Troubleshooting and Lessons Learned

Issues encountered during deployment were resolved using structured troubleshooting methods, including:

- Zabbix server and agent log analysis
- Database authentication troubleshooting
- Network interface and routing validation
- Service dependency verification

Reinstallation was intentionally avoided in favor of controlled troubleshooting to better reflect real-world operational practices.

## Documentation Structure
Supporting documentation, configuration notes, and screenshots are available in the `/docs` and `/screenshots` directories.

## Skills Demonstrated

- Linux server administration (Ubuntu Server)
- Centralized infrastructure monitoring
- Cross-platform agent deployment (Windows and Linux)
- Service availability and dependency monitoring
- Network segmentation and static IP design
- Alert design and operational visibility
- Log analysis and structured troubleshooting
- Enterprise-grade technical documentation
