# awscommunity2023-repo
This is a demo presented during AWS Community Day 2023 Colombia in August 12th 2023 in Bogotá, Colombia.

Talk name: Automatizando Infraestructura con DevOps

# WebApp Architecture
- Tiers: Web, Application and database.
- Environmets: Development and production.
- Serivces: Amazon Application Load Balancer, Amazon EC2, Amazon RDS, AWS CodeCommit and AWS CodePipeline.
- CloudFormation stacks: Pipeline, EC2 Instance, ALB and RDS Databse.

# Preparing the environment
1. Create a VPC network with 2 public subnets and 2 private subnets.
2. Create 2 RDS DB subnet groups:
    - A subnet group with a private subnet for dev environmet with name "dev-db-subnets"
    - A subnet group with a private subnet for prod environmet with name "prod-db-subnets" 

# Editing the parameters templates
1. Edit params-alb-dev.json and params-alb-prod.json with correct parameters:
    - pVPCId: The VPC Id network created. 
    - pSubnets: The subnet Id from public subnets created. You can split multiple subnets with a comma.
    - EC2StackName: The name of EC2 Stack. ¡Do not change!
2. Edit params-rds-dev.json and params-rds-prod.json with correct parameters:
    - pEnvironment : The environtment for stack.  "dev" for development and "prod" for production.
    - pDBName : The name for mariadb database.
    - pAllocatedStorage : The allocated storage for RDS database. You must to input a integer number.
    - pMaxAllocatedStorage:The max allocated storage for RDS database. You must to input a integer number.
    - pVPCId : The VPC Id network created. 
    - EC2StackName: The name of EC2 Stack. ¡Do not change!

# Deploying CloudFormation Stacks with pipeline and WebApp infrastrucure
1. Create a repository in AWS CodeCommit and push the template files. 
2. Create a CloudFormation stack with template basic-pipeline.yml 
3. You can see the pipeline deployed in CodePipeline and resources deployed in CloudFormation.

# Cleaning resources
1. Delete RDS CloudFormation stack.
2. Delete ALB CloudFormation stack.
3. Delete EC2 CloudFormation stack.
4. Empty the S3 bucket with the name similar to <pipilie-stackname>-artifactstorebucket-xxxx
5. Delete Pipeline CloudFormation stack.