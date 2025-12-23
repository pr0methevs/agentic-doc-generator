# 7. Monitoring & Observability

## 7.1 Application Performance
**Context:** APM tools.

- **AppDynamics:** [Dashboard Link]
- **Dynatrace:** [Dashboard Link]

## 7.2 Logging - Monitoring - Alerts
**Context:** Log aggregation and alerting policies.

- **Splunk Index:** `[index_name]`
- **Alert Channel:** `[Teams/Email]`

## 7.3 Useful Queries - Splunk / DynaTrace
**Context:** Troubleshooting search strings.

```splunk
index=[index_name] "error" | stats count by message
```
