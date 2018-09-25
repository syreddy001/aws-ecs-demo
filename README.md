Step1:
-----
Login into the demo repo and run the following command to create AWS ECS cluster in east region

aws cloudformation create-stack --template-body file://ecs-cluster.template \
--stack-name EcsClusterStack \
--capabilities CAPABILITY_IAM \
--tags Key=Name,Value=ECS \
--region us-east-1 \
--parameters ParameterKey=KeyName,ParameterValue=aws-yreddy-devops001 ParameterKey=EcsCluster,ParameterValue=getting-started ParameterKey=AsgMaxSize,ParameterValue=2

Step2:
-----
Check the status of the Cluster and make sure its complete

aws cloudformation describe-stacks --stack-name EcsClusterStack --query 'Stacks[*].[StackId, StackStatus]'


Step3:
-----
aws cloudformation create-stack --template-body file://ecs-jenkins-demo.template \
--stack-name JenkinsStack \
--capabilities CAPABILITY_IAM \
--tags Key=Name,Value=Jenkins \
--region us-east-1 \
--parameters ParameterKey=EcsStackName,ParameterValue=EcsClusterStack

Step4:
-----
aws cloudformation describe-stacks --stack-name JenkinsStack --query 'Stacks[*].[StackId, StackStatus]'
