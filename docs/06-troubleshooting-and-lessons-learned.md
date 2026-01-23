# Troubleshooting and Lessons Learned

## FS01 Performance Counter Issue

During initial onboarding of the file server, Windows performance counters were not immediately available to the Zabbix agent.

### Impact

- Incomplete metric collection
- Delayed visibility into system performance

### Resolution

- Performance counter availability was restored at the OS level
- Zabbix agent metrics normalized without template modification

### Lesson

Monitoring systems are dependent on the health and configuration of the underlying OS. Agent deployment alone does not guarantee visibility.

## Key Takeaways

- Monitoring readiness is a system responsibility, not just a tooling concern
- Baseline establishment is critical before alert tuning
- Clear documentation simplifies troubleshooting and future expansion
