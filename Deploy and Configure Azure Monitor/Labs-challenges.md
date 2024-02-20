# Exercise: Prepare your Azure Environment

Tasks:

## Task 1: Create a Log Analytics workspace.

- Configure Log Analytics data retention and archive policies.
- Enable access to a Log Analytics workspace.

### Task 1 details:

We have recently started using Azure to host various web apps. We now want to implement a centralized strategy for monitoring and alerting by using Azure Monitor.

This is your task:

You need to create and configure a Log Analytics workspace named LogAnalytics1 that meets the following requirements:

- Data must be retained for 60 days.
- Ensure that the 38055168-AppLogExaminers group has read access to all the logs in LogAnalytics1.
- Ensure that the maximum amount of data collected per day does NOT exceed 200 GB.

## Task 2: Configure logging for AzureWebApp1-38055168.

- Collect monitoring data by using Application Insights. The data must be logged to LogAnalytics1.
- Ensure that logging for the .NET core Snapshot Debugger is disabled.
- Enable file and configuration change tracking for AzureWebApp1-38055168.
- Ensure that the HTTP logs for AzureWebApp1-38055168 are sent to LogAnalytics1.
- Ensure that the SQL Insights data for the Azure SQL database used by the web app is sent to LogAnalytics1.

## Task 3: Collect telemetry data from VM1.

- Use the Azure Monitor Agent to collect telemetry data from VM1 and log it to LogAnalytics1.
- Create a data collection rule (DCR) that logs the following data:
    - IIS logs
    - Audit failure events from the Security event log
    - Critical and error events from the System event log
    - Critical and error events from the Application event log
- Enable VM insights.
- Monitor HTTP availability to the public IP address of VM1 from the public IP address of Linux-VM. The data must be logged to LogAnalytics1.

## Task 4: Configure email alerts for abnormal conditions.

- Create an action group named AG1 that sends notifications to alerts@contoso.com.
- Create an alert rule that monitors when the average percentage CPU of Linux-VM exceeds 80. When the alert is triggered, it must send an email to alerts@contoso.com.
