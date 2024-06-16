# Metrics-MEM-DISK_CLOUDWATCHCertainly! Here is the structured content for your GitHub README file:

markdown
Copy code
# Configure AWS CloudWatch Agent for Memory Metrics

In this tutorial, we are going to configure AWS CloudWatch Agent service for EC2 memory logs.

## Prerequisites

1. Ubuntu Operating System
2. IAM Role
3. `amazon-cloudwatch-agent.deb` Package

## Steps

### Step 1: Launch an EC2 Instance with Ubuntu OS

### Step 2: Create an IAM Role and Attach it to the EC2 Instance

- Create an IAM role and attach the `CloudWatchAgentServerPolicy` permission.
- Attach the IAM role to the EC2 instance:  
  `Action` > `Security` > `Modify IAM role`

### Step 3: Download the CloudWatch Agent Package

```sh
$ wget https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb
Step 4: Install the Package
sh
Copy code
$ sudo dpkg -i -E ./amazon-cloudwatch-agent.deb
Step 5: Update Packages & Install collectd
sh
Copy code
$ sudo apt-get update && sudo apt-get install collectd
Step 6: Create the CloudWatch Agent Configuration File
sh
Copy code
$ /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
Configuration Wizard Prompts:

On which OS are you planning to use the agent?
default choice: [1]
Enter 1
Are you using EC2 or On-Premises hosts?
default choice: [2]
Enter 1
Which user are you planning to run the agent?
default choice: [1]
Enter 1
Do you want to turn on StatsD daemon?
default choice: [1]
Enter 2
Do you want to monitor metrics from CollectD?
default choice: [1]
Enter 2
Do you want to monitor any host metrics? e.g. CPU, memory, etc.
default choice: [1]
Enter 1
Do you want to monitor CPU metrics per core? Additional CloudWatch charges may apply.
default choice: [1]
Enter 2
Do you want to add EC2 dimensions (ImageId, InstanceId, InstanceType, AutoScalingGroupName) into all of your metrics if the info is available?
default choice: [1]
Enter 2
Would you like to collect your metrics at high resolution (sub-minute resolution)?
default choice: [4]
Enter 4
Which default metrics config do you want?
default choice: [1]
Enter 1
Are you satisfied with the above config? Note: it can be manually customized after the wizard completes to add additional items.
default choice: [1]
Enter 1
Do you have any existing CloudWatch Log Agent configuration file to import for migration?
default choice: [2]
Enter 2
Do you want to monitor any log files?
default choice: [1]
Enter 2
The config file is located at /opt/aws/amazon-cloudwatch-agent/bin/config.json (edit manually if needed).

Step 7: Check the Status of the CloudWatch Agent Service
sh
Copy code
$ /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status
Step 8: Start the Service and Check Status
sh
Copy code
$ /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -s -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json
Step 9: Check Custom Metrics in AWS CloudWatch
Navigate to CloudWatch > Metrics > CWAgent

Step 10: Verify Memory Metrics on the Host


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

set these values to no

> Do you want to turn on StatsD daemon?
no

> Do you want to monitor metrics from CollectD? WARNING: CollectD must be installed or the Agent will fail to start
no

> Do you have any existing CloudWatch Log Agent (http://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AgentReference.html) configuration file to import for migration?
no

> Do you want to monitor any log files?
no

> Do you want the CloudWatch agent to also retrieve X-ray traces?
no
