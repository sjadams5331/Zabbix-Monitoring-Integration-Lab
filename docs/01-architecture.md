# Architecture and Monitoring Design

## Overview

This monitoring environment was designed to reflect how a centralized NOC monitors critical services across mixed operating systems and workloads.

Zabbix was positioned as a visibility and alerting layer rather than a configuration management or analytics platform. Monitoring decisions were guided by operational relevance, service dependency, and signal quality.

## Architecture Summary

- Zabbix Server: `zabbix01` (Ubuntu Server)
- Web Frontend: Apache
- Database Backend: MariaDB
- Monitoring Method: Zabbix Agent (active and passive checks)
- Network: VirtualBox host-only network with static IP addressing

Agents communicated with the Zabbix server over TCP 10050, while the server processed and coordinated checks on TCP 10051.

## Dependency Awareness

Monitoring was designed with the following dependencies in mind:

- Authentication services (Active Directory) underpin access to applications
- File services support user workflows and application storage
- The helpdesk application represents a user-facing service dependent on underlying infrastructure

Alerts were evaluated not only in isolation, but in terms of how failures could cascade across systems.
