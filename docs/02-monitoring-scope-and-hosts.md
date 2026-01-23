# Monitoring Scope and Hosts

## Monitoring Scope

Monitoring focused on availability, resource utilization, and service health rather than exhaustive metric collection.

The intent was to ensure that:
- Core services remained reachable
- Resource exhaustion was detected before service impact
- Alerts reflected actionable conditions

## Monitored Hosts

### DC01 – Domain Controller

- Operating System: Windows Server
- Role: Active Directory Domain Services
- Monitoring Method: Zabbix Agent (Windows)
- Template: Windows by Zabbix agent

Monitored aspects included host availability, CPU and memory utilization, and core system health indicators relevant to directory services.

### FS01 – File Server

- Operating System: Windows Server
- Role: File Server
- Monitoring Method: Zabbix Agent (Windows)
- Template: Windows by Zabbix agent

This host was used to demonstrate monitoring of infrastructure services and storage-related metrics. Initial onboarding exposed Windows performance counter issues that required remediation prior to full metric collection.

### osticket01 – Helpdesk Application Server

- Operating System: Debian GNU/Linux 12
- Role: osTicket Application Server
- Monitoring Method: Zabbix Agent (Linux)
- Template: Linux by Zabbix agent

Monitoring focused on system health and availability to support a user-facing service.
