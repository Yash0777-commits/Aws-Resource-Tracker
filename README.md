# AWS Resource Tracker

This project provides a script to list and display key details about AWS resources, including:
- S3 Buckets
- EC2 Instances
- Lambda Functions
- IAM Users

The script is designed to automate the collection of AWS resource information and store the results in a log file for easy access and monitoring.

---

## Features

- Fetches and displays the following AWS resource information:
  - **S3 Buckets**: Lists all S3 buckets in your AWS account.
  - **EC2 Instances**: Details include Instance ID, State, Type, Public IP, and Private IP.
  - **Lambda Functions**: Details include Function Name, Runtime, Handler, and Last Modified date.
  - **IAM Users**: Details include User Name, Creation Date, and ARN.
- Saves the output to a log file for record-keeping.
- Can be scheduled using cron jobs for periodic execution.

---

## Requirements

1. **AWS CLI** installed and configured.
2. Proper IAM permissions for the AWS CLI user.
3. Linux environment with Bash.
4. `jq` utility installed for JSON processing.

---

## Step-by-Step Guide

### Step 1: Install AWS CLI

1. Download the AWS CLI:
   ```bash
   sudo apt update
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
   unzip awscliv2.zip
   sudo ./aws/install
   ```

2. Verify the installation:
   ```bash
   aws --version
   ```

3. Configure AWS CLI with your credentials:
   ```bash
   aws configure
   ```
   Provide:
   - Access Key ID
   - Secret Access Key
   - Default region
   - Output format (e.g., `json` or `table`)

### Step 2: Install `jq`

`jq` is required for processing JSON outputs:
```bash
sudo apt install jq -y
```

### Step 3: Create the Script

1. Create a Bash script file:
   ```bash
   nano aws_resource_tracker.sh
   ```

2. Add the following content to the script:
   ```bash
   #!/bin/bash
   set -e

   LOG_FILE="/path/to/your/logs/aws_resource_tracker.log"

   # AWS S3
   echo "Fetching AWS S3 Buckets List..." >> $LOG_FILE
   aws s3 ls >> $LOG_FILE 2>&1

   # AWS EC2
   echo "Fetching AWS EC2 Instances List..." >> $LOG_FILE
   aws ec2 describe-instances --query "Reservations[*].Instances[*].{ID:InstanceId,State:State.Name,Type:InstanceType,PublicIP:PublicIpAddress,PrivateIP:PrivateIpAddress}" --output table >> $LOG_FILE 2>&1

   # AWS Lambda
   echo "Fetching AWS Lambda Functions List..." >> $LOG_FILE
   aws lambda list-functions --query "Functions[*].{FunctionName:FunctionName,Runtime:Runtime,Handler:Handler,LastModified:LastModified}" --output table >> $LOG_FILE 2>&1

   # AWS IAM Users
   echo "Fetching AWS IAM Users List..." >> $LOG_FILE
   aws iam list-users --query "Users[*].{UserName:UserName,CreateDate:CreateDate,Arn:Arn}" --output table >> $LOG_FILE 2>&1
   ```

3. Save and close the file.
4. Make the script executable:
   ```bash
   chmod +x aws_resource_tracker.sh
   ```

### Step 4: Test the Script

Run the script manually to ensure it works as expected:
```bash
./aws_resource_tracker.sh
```

Verify the log file contains the desired output.

### Step 5: Automate with Cron Job

1. Open the crontab editor:
   ```bash
   crontab -e
   ```

2. Add the following line to execute the script every hour:
   ```bash
   0 * * * * /bin/bash /path/to/aws_resource_tracker.sh >> /path/to/your/logs/aws_resource_tracker.log 2>&1
   ```

3. Save and close the editor.

### Step 6: Push Project to GitHub

1. Initialize a Git repository in your project directory:
   ```bash
   git init
   ```

2. Add all files:
   ```bash
   git add .
   ```

3. Commit the changes:
   ```bash
   git commit -m "Initial commit"
   ```

4. Create a new repository on GitHub.

5. Link your local repository to GitHub:
   ```bash
   git remote add origin https://github.com/YourUsername/aws-resource-tracker.git
   ```

6. Push your code to GitHub:
   ```bash
   git branch -M main
   git push -u origin main
   ```

---

## Troubleshooting

1. **Permission Errors**:
   - Ensure your AWS CLI user has appropriate permissions for S3, EC2, Lambda, and IAM.

2. **Cron Job Not Running**:
   - Check the cron logs using:
     ```bash
     grep CRON /var/log/syslog
     ```

3. **Log File Issues**:
   - Ensure the specified log file path exists and is writable.

---

## Contribution
Feel free to contribute to this project by submitting issues or pull requests on GitHub.

---

## License
This project is licensed under the MIT License.

