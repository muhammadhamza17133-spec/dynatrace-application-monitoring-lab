# Dynatrace Query Language (DQL) Practice

Here are the core DQL queries used during my lab investigation and log analysis.

### 1. Retrieve Recent Logs
Purpose: To get a quick overview of the most recent log records in the environment.

fetch logs
| limit 20


### 2. Filter for Error Logs
Purpose: To isolate only ERROR level logs and extract specific fields (timestamp, log level, host, and content) for troubleshooting.

fetch logs
| filter loglevel == "ERROR"
| fields timestamp, loglevel, dt.entity.host, content
| limit 20


### 3. Aggregate Log Counts by Level
Purpose: To summarize large volumes of log data (over 380,000 records) and group them by log level (DEBUG, INFO, ERROR, WARN) to identify how noisy the system is.

fetch logs
| summarize records = count(), by: {loglevel}
| sort records desc
