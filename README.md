
# AWS Resource Tracker

This project is a shell script that tracks and retrieves details about AWS resources such as S3 buckets, EC2 instances, Lambda functions, and IAM users. The output is logged in a structured format for better usability.

---

## Features

- Fetch and list AWS S3 buckets.
- Retrieve details about AWS EC2 instances (Instance ID, State, Type, Public IP, Private IP).
- Fetch AWS Lambda functions (Name, Runtime, Handler, Last Modified date).
- Retrieve AWS IAM users (Username, Creation Date, ARN).
- Logs all outputs to a specified log file.

---

## Prerequisites

- **AWS CLI** installed and configured with proper access credentials.
- **jq** package installed for JSON parsing.

To install jq:
```bash
sudo apt install jq
```

---

## Script Usage

### 1. Setup

Place the script in your project directory, e.g., `aws_resource_tracker.sh`.

### 2. Configure Log File

Edit the script to define the log file path:
```bash
LOG_FILE="/path/to/your/logs/aws_resource_tracker.log"
```

### 3. Execute the Script

Run the script:
```bash
bash aws_resource_tracker.sh
```

### Example Output

#### S3 Buckets:
```
Fetching AWS S3 Buckets List...
2023-12-19 12:00:00 bucket-name-1
2023-12-19 12:00:00 bucket-name-2
```

#### EC2 Instances:
```
+-----------------+---------+-----------+-----------+------------+
|       ID        | State   |   Type    | PublicIP  | PrivateIP  |
+-----------------+---------+-----------+-----------+------------+
| i-12345abcdef   | running | t2.micro  | 3.3.3.3   | 10.0.0.1   |
+-----------------+---------+-----------+-----------+------------+
```

---

## Automation with Cron Jobs

Automate the script execution using cron jobs. 

### Cron Job Setup

Edit the crontab:
```bash
crontab -e
```

Add the following line to run the script every day at midnight:
```bash
0 0 * * * /bin/bash /path/to/aws_resource_tracker.sh >> /path/to/your/logs/aws_resource_tracker.log 2>&1
```

### Verify Cron Job Execution

Check the logs to confirm successful execution:
```bash
cat /path/to/your/logs/aws_resource_tracker.log
```

---

## Error Handling

Errors from AWS CLI commands are redirected to the log file for debugging.

---

## GitHub Repository Setup

### 1. Initialize a New Repository

Run the following commands in the project directory:
```bash
git init
git add .
git commit -m "Initial commit of AWS Resource Tracker"
git branch -M main
git remote add origin <repository-url>
git push -u origin main
```

Replace `<repository-url>` with your GitHub repository URL.

### 2. View README

The `README.md` file will be displayed on the main page of the GitHub repository.

---

## License

This project is licensed under the MIT License.
