# Wordpress Containers and RDS Cloudformation stack

Example setup of Containerized Wordpress on AWS RDS mysql.

## sync nested template to S3
aws s3 cp ./fargate-security.yaml s3://sandbox01-demo-iad/templates/
aws s3 cp ./fargate-ecs.yaml s3://sandbox01-demo-iad/templates/
aws s3 cp ./fargate-rds.yaml s3://sandbox01-demo-iad/templates/

