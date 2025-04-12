# aws-cli-examples-all-services

Here is an **updated comprehensive list of AWS CLI commands** covering **creation**, **configuration**, and **modification** for major AWS services, organized by service type:

---

## **1. AWS CLI Setup & Configuration**
```bash
aws configure                            # Set access key, secret, region, output
aws configure get region                 # Get default region
aws configure set region ap-south-1      # Set default region
aws sts get-caller-identity              # Check identity
```

---

## **2. EC2 – Instances, Security Groups, and Key Pairs**
### Create & Launch Instance
```bash
aws ec2 create-key-pair --key-name MyKey --query 'KeyMaterial' --output text > MyKey.pem
aws ec2 create-security-group --group-name MySG --description "My SG"
aws ec2 run-instances \
  --image-id ami-0abcdef1234567890 \
  --count 1 \
  --instance-type t2.micro \
  --key-name MyKey \
  --security-groups MySG
```

### Modify
```bash
aws ec2 modify-instance-attribute --instance-id i-xxxxxx --instance-type "{\"Value\": \"t3.micro\"}"
aws ec2 associate-address --instance-id i-xxxxxx --public-ip 1.2.3.4
```

---

## **3. S3 – Bucket Management**
### Create & Upload
```bash
aws s3 mb s3://my-bucket-name
aws s3 cp myfile.txt s3://my-bucket-name/
```

### Configure
```bash
aws s3api put-bucket-versioning --bucket my-bucket-name --versioning-configuration Status=Enabled
aws s3api put-bucket-policy --bucket my-bucket-name --policy file://policy.json
```

---

## **4. IAM – Users, Roles, Policies**
### Create
```bash
aws iam create-user --user-name myuser
aws iam create-role --role-name myrole --assume-role-policy-document file://trust.json
aws iam put-user-policy --user-name myuser --policy-name AdminPolicy --policy-document file://adminpolicy.json
```

### Modify
```bash
aws iam update-user --user-name myuser --new-user-name newusername
aws iam attach-user-policy --user-name myuser --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
```

---

## **5. Lambda – Function Management**
### Create & Update
```bash
aws lambda create-function \
  --function-name myfunction \
  --runtime python3.9 \
  --role arn:aws:iam::123456789012:role/myrole \
  --handler lambda_function.lambda_handler \
  --zip-file fileb://function.zip

aws lambda update-function-code \
  --function-name myfunction \
  --zip-file fileb://updated_function.zip
```

---

## **6. RDS – Database Instances**
### Create
```bash
aws rds create-db-instance \
  --db-instance-identifier mydb \
  --db-instance-class db.t2.micro \
  --engine mysql \
  --master-username admin \
  --master-user-password password123 \
  --allocated-storage 20
```

### Modify
```bash
aws rds modify-db-instance \
  --db-instance-identifier mydb \
  --apply-immediately \
  --backup-retention-period 7
```

---

## **7. CloudFormation – Stack Management**
```bash
aws cloudformation create-stack --stack-name mystack --template-body file://template.yaml
aws cloudformation update-stack --stack-name mystack --template-body file://updated_template.yaml
aws cloudformation delete-stack --stack-name mystack
```

---

## **8. ECR – Docker Registry**
```bash
aws ecr create-repository --repository-name myrepo
aws ecr put-lifecycle-policy --repository-name myrepo --lifecycle-policy-text file://policy.json
```

---

## **9. ECS – Container Services**
```bash
aws ecs create-cluster --cluster-name my-cluster
aws ecs register-task-definition --cli-input-json file://task-def.json
aws ecs create-service --cli-input-json file://service-def.json
aws ecs update-service --cluster my-cluster --service my-service --desired-count 2
```

---

## **10. CodePipeline / CodeBuild / CodeDeploy**
### CodePipeline
```bash
aws codepipeline create-pipeline --cli-input-json file://pipeline.json
aws codepipeline update-pipeline --cli-input-json file://updated-pipeline.json
```

### CodeBuild
```bash
aws codebuild create-project --cli-input-json file://buildproject.json
aws codebuild update-project --cli-input-json file://updated_buildproject.json
```

### CodeDeploy
```bash
aws deploy create-application --application-name MyApp
aws deploy create-deployment-group --application-name MyApp --deployment-group-name MyDG ...
```

---

## **11. CloudWatch – Monitoring and Logs**
```bash
aws logs create-log-group --log-group-name my-log-group
aws logs create-log-stream --log-group-name my-log-group --log-stream-name my-stream
aws logs put-log-events --log-group-name my-log-group --log-stream-name my-stream --log-events file://logs.json
```

---

## **12. SNS – Notifications**
```bash
aws sns create-topic --name my-topic
aws sns subscribe --topic-arn arn:aws:sns:... --protocol email --notification-endpoint my@example.com
aws sns publish --topic-arn arn:aws:sns:... --message "Hello"
```

---

## **13. SQS – Queueing**
```bash
aws sqs create-queue --queue-name my-queue
aws sqs send-message --queue-url https://... --message-body "Hello SQS"
```

---

Would you like this organized in a **PDF or Markdown file** for distribution or training purposes? Or do you want to build a GitHub repo with working examples of each?
