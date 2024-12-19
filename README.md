# AWS Resource Tracker

A Bash script to track and log various AWS resources, such as S3 buckets, EC2 instances, Lambda functions, and IAM users. This script fetches the details of these resources and saves the output to a specified log file for easy access and analysis.

## Features
- List all S3 buckets in your AWS account.
- Display information about EC2 instances, including their state, instance type, public/private IP addresses.
- Show details of Lambda functions, such as function name, runtime, handler, and last modified time.
- Fetch IAM user details, including usernames, creation dates, and ARNs.
- Logs all output to a specified file for future reference.

## Prerequisites
1. **AWS CLI**: Ensure the AWS CLI is installed and configured on your system.  
   To install the AWS CLI on Ubuntu, run:
   sudo apt update
   sudo apt install awscli -y
