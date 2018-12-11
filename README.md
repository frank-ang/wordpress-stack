# Wordpress Containers and RDS Cloudformation stack

Example setup of Containerized Wordpress on AWS RDS MySQL.

## Setup instructions

### 1. Push my-wordpress container to ECR

Dependency on my-wordpress container repo. Build and push. The repo name should be "my-wordpress".

See:
https://github.com/frank-ang/my-wordpress

### 2. Upload nested templates to S3

```
aws s3 cp ./fargate-security.yaml s3://sandbox01-demo-iad/templates/
aws s3 cp ./fargate-ecs.yaml s3://sandbox01-demo-iad/templates/
aws s3 cp ./fargate-rds.yaml s3://sandbox01-demo-iad/templates/
```

### 3. Create stacks

```
aws cloudformation create-stack --stack-name [STACKNAME] --template-body file://./fargate-top.yaml  \
--capabilities CAPABILITY_NAMED_IAM \
--parameters \
ParameterKey=VPC,ParameterValue=[VPC_ID] \
ParameterKey=SubnetA,ParameterValue=[SUBNET1] \
ParameterKey=SubnetB,ParameterValue=[SUBNET2] \
ParameterKey=ServiceName,ParameterValue=my-wordpress \
ParameterKey=Image,ParameterValue=[ACCOUNTID].dkr.ecr.us-east-1.amazonaws.com/my-wordpress:[commit] \
ParameterKey=DatabaseInstanceClass,ParameterValue=db.t2.small \
ParameterKey=DatabasePassword,ParameterValue=[ADMIN_PASSWORD] \
ParameterKey=DatabaseUser,ParameterValue=[ADMIN_USERNAME]
```

### 4. Initialize wordpress
Get the ALB URL output for the stack, Login to WP and configure hostname to the LB endpoint.