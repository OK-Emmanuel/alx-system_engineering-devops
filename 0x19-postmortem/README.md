# Postmortem Report

## Error 503: Service Unavailable
<img src="./Postmortem report.jpg">

### Issue Summary
**Duration of Outage:**  
- Start Time: June 5, 2024, 10:00 AM (UTC)  
- End Time: June 5, 2024, 12:30 PM (UTC)  

**Impact:**  
- Service Down: Main web application was inaccessible.  
- User Experience: Users encountered 503 Service Unavailable errors.  
- Affected Users: 85% of total user base experienced the outage.

**Root Cause:**  
- A misconfiguration in the load balancer led to an unexpected increase in traffic to a single server, causing it to crash.

### Timeline

- **10:00 AM:** Issue detected via monitoring alert indicating a spike in 503 errors.
- **10:05 AM:** Engineering team alerted through automated paging system.
- **10:10 AM:** Initial investigation started; assumption was a potential database issue due to similar past incidents.
- **10:25 AM:** Database team confirmed no issues; attention shifted to the application servers.
- **10:40 AM:** Misleading path: checked recent application code deployments but found no errors.
- **11:00 AM:** Network team investigated and identified a misconfiguration in the load balancer.
- **11:15 AM:** Incident escalated to the DevOps team.
- **11:30 AM:** DevOps team began reconfiguring the load balancer.
- **12:00 PM:** Load balancer configuration corrected and services started to recover.
- **12:30 PM:** Full service restoration confirmed; monitoring continued to ensure stability.

### Root Cause and Resolution

**Root Cause:**  
The issue was traced to a recent update in the load balancer configuration. A parameter that controls traffic distribution was incorrectly set, directing the majority of incoming traffic to a single application server. This server became overwhelmed, leading to its failure and the resulting 503 errors for users.

**Resolution:**  
The load balancer configuration was reviewed and corrected to ensure even traffic distribution across all application servers. The DevOps team implemented a rolling restart of the application servers to restore full functionality. Continuous monitoring was employed to confirm that the service was stable post-resolution.

### Corrective and Preventative Measures

**Improvements and Fixes:**  
1. **Configuration Management:** Review and tighten the configuration change process for critical infrastructure components such as load balancers.
2. **Enhanced Monitoring:** Implement more granular monitoring for load balancer configurations and traffic distribution.
3. **Training:** Conduct regular training sessions for the engineering and DevOps teams on best practices for configuration management and issue detection.

**Specific Tasks:**
1. **Review Load Balancer Configuration:** Conduct a comprehensive review of all load balancer settings and ensure they adhere to best practices.
2. **Add Monitoring Alerts:** Set up alerts for unusual traffic patterns and load balancer configurations.
3. **Implement Configuration Audits:** Establish regular automated audits of configuration changes for critical components.
4. **Update Incident Response Plan:** Revise the incident response plan to include steps for quicker identification and resolution of load balancer-related issues.
5. **Documentation:** Improve documentation for load balancer configurations and common troubleshooting steps.
6. **Training Session:** Schedule and conduct a training session focused on configuration management and monitoring.

By implementing these measures, we aim to reduce the likelihood of similar incidents and improve our response time for any future issues.