# EC2 Instance Scheduler with Slack Notifications

## Overview
This CloudFormation template creates an automated EC2 instance scheduler using AWS Lambda and EventBridge. It helps reduce AWS costs by automatically starting and stopping non-production instances based on defined working hours. Additionally, it includes a resource-checking Lambda function that identifies untagged resources and sends notifications via Slack.

## Features
- **Automated Scheduling**: Uses EventBridge to trigger Lambda functions for starting and stopping instances.
- **Tag-Based Control**: Only instances tagged with `AutoStop: true` are affected.
- **Slack Notifications**: Notifies a Slack channel whenever instances are started or stopped.
- **Daily Resource Audit**: Checks for untagged EC2 instances, EBS volumes, and Elastic IPs, sending a report to Slack.
- **Production-Safe**: Ensures production workloads remain unaffected.

## Cost Savings Example
- Monthly EC2 costs reduced from **$8,500 to $3,145**.
- Identified **$950 worth of untagged resources** in the first week.

## Deployment
### Prerequisites
- AWS account with appropriate IAM permissions.
- Slack Webhook URL for notifications.

### Steps
1. Deploy the CloudFormation template.
2. Provide working hours (UTC format) for instance start/stop times.
3. Add the `AutoStop: true` tag to all non-production instances.
4. Monitor Slack notifications for instance actions and untagged resources.

## CloudFormation Template
This repository contains a CloudFormation YAML file that defines:
- An IAM role with permissions for EC2 and Lambda.
- Two Lambda functions:
  - `InstanceSchedulerFunction` for managing EC2 instances.
  - `UntaggedResourcesFunction` for identifying untagged resources.
- EventBridge rules to trigger Lambda functions on schedule.
- Slack integration for automated notifications.

## Customization
Modify the `WorkingHoursStart` and `WorkingHoursEnd` parameters in the CloudFormation template to adjust instance schedules.

## How It Works
1. **Instance Scheduling**:
   - At `WorkingHoursStart`, Lambda starts all tagged instances.
   - At `WorkingHoursEnd`, Lambda stops all tagged instances.
   - Sends a notification to Slack.
2. **Daily Resource Audit**:
   - Scans EC2 instances, EBS volumes, and Elastic IPs for missing tags.
   - Sends a Slack report listing untagged resources.

## Next Steps
- Deploy the CloudFormation stack.
- Tag your instances appropriately.
- Monitor Slack for instance activity and untagged resources.

## Contributing
Feel free to submit pull requests for improvements!

## License(s)
MIT

