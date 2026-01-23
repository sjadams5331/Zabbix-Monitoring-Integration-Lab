# Monitoring Scope and Hosts

## Monitoring Scope Overview

The monitoring scope for this environment was intentionally constrained to reflect how enterprise NOCs prioritize signal quality over metric quantity.

Rather than collecting every possible datapoint, monitoring focused on conditions that directly affect service availability, stability, and user impact. This approach reduces alert fatigue and ensures that generated alerts correspond to conditions that warrant investigation or action.

The scope was designed to answer three primary operational questions:

- Are critical systems reachable?
- Are core resources approaching exhaustion?
- Are foundational services behaving as expected?

## Monitoring Boundaries

This environment does not attempt to replace:
- Performance engineering tools
- Capacity planning platforms
- Log aggregation or SIEM solutions

Zabbix was used strictly as a **real-time monitoring and alerting system**, consistent with how it is commonly deployed in NOC environments.

Historical trend analysis and deep diagnostics are intentionally secondary to immediate visibility and alerting accuracy.

## Monitored Hosts

![Monitored Hosts](..screenshots/hosts.png)

### DC01 – Active Directory Domain Controller

- **Operating System:** Windows Server  
- **Role:** Active Directory Domain Services  
- **Monitoring Method:** Zabbix Agent (Windows)  
- **Template:** Windows by Zabbix agent  

DC01 represents a foundational dependency within the environment. Its availability directly impacts authentication, authorization, and access to downstream services.

Monitoring coverage emphasized:
- Host availability
- CPU and memory utilization
- Core system health indicators relevant to directory services

The intent was to ensure early visibility into conditions that could degrade authentication services rather than to monitor directory internals exhaustively.

### FS01 – File Server

- **Operating System:** Windows Server  
- **Role:** File Server  
- **Monitoring Method:** Zabbix Agent (Windows)  
- **Template:** Windows by Zabbix agent  

FS01 was included to represent shared infrastructure services commonly relied upon by users and applications.

Monitoring focused on:
- Host availability
- Resource utilization
- Storage-related metrics exposed through standard Windows performance counters

During initial onboarding, incomplete metric collection highlighted the dependency between monitoring tools and OS-level instrumentation. Once resolved, FS01 provided consistent and reliable infrastructure telemetry.

This host serves as an example of how monitoring can surface environmental readiness issues in addition to runtime health concerns.

### osticket01 – Helpdesk Application Server

- **Operating System:** Debian GNU/Linux 12  
- **Role:** osTicket Helpdesk Application Server  
- **Monitoring Method:** Zabbix Agent (Linux)  
- **Template:** Linux by Zabbix agent  

osticket01 represents a user-facing service with dependencies on both identity and infrastructure layers.

Monitoring emphasized:
- Host availability
- CPU and memory utilization
- General system health

Application-level monitoring was intentionally minimal. The goal was to validate platform stability rather than inspect application internals, mirroring environments where application monitoring is layered on incrementally.

### zabbix01 – Monitoring Server

- **Operating System:** Ubuntu Server  
- **Role:** Zabbix Monitoring Platform  
- **Monitoring Method:** Zabbix Agent (Linux)  
- **Template:** Linux by Zabbix agent  

The monitoring platform was treated as a first-class system and monitored alongside all other hosts.

Self-monitoring ensured:
- Visibility into monitoring system health
- Early detection of resource pressure affecting alerting
- Confidence that monitoring failures would be observable

This reflects standard NOC practice where monitoring infrastructure is considered production-critical.

## Host Classification and Consistency

All hosts were onboarded using:
- Consistent naming conventions
- Static IP addressing
- Role-appropriate templates
- Agent-based monitoring

This consistency simplifies operational reasoning and reduces ambiguity during incident triage.

Hosts were monitored based on **what they provide**, not merely what operating system they run. This reinforces service-oriented thinking rather than asset-centric monitoring.

## Scope Summary

The monitoring scope was deliberately limited to support:
- High signal-to-noise alerting
- Clear service dependency visibility
- Predictable and stable monitoring behavior

By avoiding over-instrumentation, the environment remains easy to interpret, maintain, and discuss during technical reviews or interviews.
