# AWS EC2 CloudWatch Monitoring & Alerting

Hands-on AWS project monitoring EC2 CPU usage with CloudWatch and triggering real-time email alerts via SNS when thresholds are breached.

## What it does

- Monitors an EC2 instance's CPU utilization using Amazon CloudWatch
- Triggers a CloudWatch Alarm when CPU usage exceeds 70% for a 5-minute period
- Sends an automated email notification via Amazon SNS when the alarm fires

## Architecture

EC2 Instance --> CloudWatch (CPUUtilization metric)
|
v
CloudWatch Alarm (threshold: 70%)
|
v
SNS Topic (ec2-cpu-alerts)
|
v
Email Notification


## How I built and tested it

1. Launched a Free Tier t3.micro EC2 instance (Amazon Linux)
2. Created an SNS topic (`ec2-cpu-alerts`) and subscribed my email
3. Created a CloudWatch Alarm on the instance's `CPUUtilization` metric:
   - Statistic: Average, Period: 5 minutes
   - Threshold: Greater than 70%
   - Action: Notify the SNS topic when "In alarm"
4. Connected to the instance via EC2 Instance Connect and installed the `stress` load-testing tool:

5. Confirmed the alarm crossed the 70% threshold and briefly entered "In alarm" state
6. Confirmed receipt of the SNS email notification
<img width="1885" height="871" alt="image" src="https://github.com/user-attachments/assets/a30c9920-047a-4197-b8ab-6db1e4e5adda" />

## What I learned

This project helped me understand how production systems are monitored in practice — not just how to configure a metric, but how alerting pipelines (metric → alarm → notification) are wired together end-to-end. It also reinforced the importance of testing monitoring setups deliberately, rather than assuming they work.

## Tools used

AWS EC2, Amazon CloudWatch, Amazon SNS, Linux (Amazon Linux), `stress` CLI tool.
