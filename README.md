
# hello world template
aws cloudformation create-stack --stack-name hello1 --template-body file://./hello-bucket.yaml  \
--parameters  ParameterKey=VPC,ParameterValue=vpc-ba429dc0 ParameterKey=ServiceName,ParameterValue=hello1 

# sync nested template to S3
aws s3 cp ./fargate-security.yaml s3://sandbox01-demo-iad/templates/
aws s3 cp ./fargate-ecs.yaml s3://sandbox01-demo-iad/templates/
aws s3 cp ./fargate-rds.yaml s3://sandbox01-demo-iad/templates/


