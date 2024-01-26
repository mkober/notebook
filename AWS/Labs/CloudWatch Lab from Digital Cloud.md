#DigitalCloudTraining 
### Create the IAM role for SSM/CloudWatch
1. Create an IAM role with an EC2 trust policy
2. Add the following managed policies
CloudWatchAgentServerPolicy
AmazonSSMManagedInstanceCore
3. Name the IAM role as below and create
CloudWatchAgentServerRole
4. Launch an EC2 instance and attach the role

### Install the CloudWatch agent using SSM Run Command
1. Choose AWS-ConfigureAWSPackage
2. Under name enter AmazonCloudWatchAgent
3. Install collectd
sudo amazon-linux-extras install collectd
4. Run the wizard on the EC2 instance command line
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
5. During the wizard specify additional log file collection
/var/log/messages
6. Run the following commmand
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
7. Then make sure the agent is started
sudo systemctl start amazon-cloudwatch-agent

### Launch instances with a tag
aws ec2 run-instances --image-id ami-0dfcb1ef8550277af --count 2 --instance-type t2.micro --tag-specifications 'ResourceType=instance,Tags=[{Key=Department,Value=Operations}]'

### CloudWatch Logs Insights query
fields @timestamp, @message | sort @timestamp desc | limit 25

### Install Apache and Configure Logging
1. If not already installed, install the CloudWatch agent
sudo yum install amazon-cloudwatch-agent
2. Also, install collectd
sudo amazon-linux-extras install collectd
3. Install and enable Apache
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd
4. If the config file exists, delete it
sudo rm -rf /opt/aws/amazon-cloudwatch-agent/bin/config.json
5. Create the config.json
sudo nano /opt/aws/amazon-cloudwatch-agent/bin/config.json
6. Add the contents from the cw-config.json file provided
7. Run the following commmand
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
8. Then make sure the agent is started
sudo systemctl start amazon-cloudwatch-agent
9. Generate some traffic to Apache including some 404s

### Create a metric filter and alarm
1. Create a metric filter and use the following pattern
[host, logName, user, timestamp, request, statusCode=404, size]
2. Define the filter and create
Name = 404
Metric namespace = HTTPStatusCode
Metric name = 404Error
Metric value = 1
Unit = Count
3. Create an alarm for the filter with count greater than 2 in 5 minutes
4. Create a new SNS Topic or use an existing one
5. Generate more 404 errors


### Create an IAM role and instance profile
1. Create an IAM policy
aws iam create-policy --policy-name "CloudWatch-Put-Metric-Data" --policy-document '{"Version":"2012-10-17","Statement":[{"Effect":"Allow","Action":["cloudwatch:PutMetricData"],"Resource":"*"}]}'
2. Create an IAM role that uses the policy document
aws iam create-role --role-name "CloudWatch-Role" --assume-role-policy-document '{"Version":"2012-10-17","Statement":[{"Effect":"Allow","Principal":{"Service":"ec2.amazonaws.com"},"Action":"sts:AssumeRole"}]}'
3. Attach the policy to the role (update policy ARN)
aws iam attach-role-policy --role-name "CloudWatch-Role" --policy-arn "arn:aws:iam::821711655051:policy/CloudWatch-Put-Metric-Data"
4. Create an instance profile
aws iam create-instance-profile --instance-profile-name "CloudWatch-Instance-Profile"
5. Add the role to the instance profile
aws iam add-role-to-instance-profile --instance-profile-name "CloudWatch-Instance-Profile" --role-name "CloudWatch-Role"

### Launch an EC2 instance
1. Create a security group
aws ec2 create-security-group --group-name CustomMetricLab --description "Temporary SG for the Custom Metric Lab"
2. Add a rule for SSH inbound to the security group
aws ec2 authorize-security-group-ingress --group-name CustomMetricLab --protocol tcp --port 22 --cidr 0.0.0.0/0
3. Launch instance in US-EAST-1A
aws ec2 run-instances --image-id ami-0aa7d40eeae50c9a9 --instance-type t2.micro --placement AvailabilityZone=us-east-1a --security-group-ids sg-0c6f4290d647e7813 --iam-instance-profile Name="CloudWatch-Instance-Profile"

### Install stress
sudo amazon-linux-extras install epel -y
sudo yum install stress-ng -y


### Run the stres utility to generate load
stress-ng --vm 15 --vm-bytes 80% --vm-method all --verify -t 60m -v
### Create an alarm in CloudWatch
1. Create an alarm that is based on the custom metric


