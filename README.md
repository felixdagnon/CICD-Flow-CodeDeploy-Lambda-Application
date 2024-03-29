# CICD Pipeline using AWS DevOps (Cloud9, CodeCommit, CodeBuild, S3, CloudFormation(SAM), Lambda, API Gateway)


Here I create CICD pipeline flow  for a serverless application. It's works in my environment.

(Always create an IAM user, and add policies according to your need. Never use root account).

Follow Best Practices for Cloud Security with AWS IAM: Managing Groups, Policies, and Roles


![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/19d85248-91dd-4967-8b06-7152609ce845)


# 1-IAM Roles and policies 

lets create some IAM role and policies that will allow us to create the pipeline.

## Create Iam role for CodeBuild

Here I created a role for codebuild named — “codebuild-s3-cloudwatch” 

Then I added “AmazonS3FullAccess” and “CloudWatchFullAccess” policy to this role.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/52368426-13b8-4101-9ffd-20346792107f)

## Create role for CodeDeploy 

Here I create another role name — “cfn-codepipeline-cft” for CodeDeploy and added two policy one is — “AWSLambdaExecute” 

and created ajson inline policy named — “policyToDeployUsingCloudFormation”. 

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/4595b200-bc15-4cdf-a0c6-a6c3755a4040)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/41736a78-569f-49be-a909-f36495651315)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/019c1e85-1d81-4a72-a953-9afae736250f)


# 2-Create S3 bucket for CodePipeline

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/39a3c393-ad68-4345-84ec-c87972f88129)


## Create CodeCommit Repo and push in the codes 

let's create a CodeCommit repository first called codepipeline-lambda-demo and push our code from Cloud9 IDE.

I will store all code in CodeCommit repository

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/802323ca-7154-4340-9907-587719e89065)

# 3-Cloud9 clone CodeCommit repo

Clone the repo in Cloud9 and upload files.

I use git commands (git add -A,  git commit -m "Add sample application file", git push)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/9dc84819-cfcb-48b7-aeb7-194a8783fde7)

# 4-Code files pushed in CodeCommit repo

Ok there are three files:

Buildspec.yml is for the CodeBuild

template.yml is the CloudFormation SAM template that will create resources like API Gateway, and Lambda. Attach the API gateway with Lambda and deploy the code into the Lambda function. 

lambda_funtion.py is the file of code that will be deployed into lambda. 

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/b0f0d02d-195b-48cc-9bf5-fda79473b1c5)

### buildspec.yml

This will be used in Codebuild and artifact wil save in a s3 bucket name “codepipeline-lambda-bucket-demo”. Create s3 bucket according to the buildspec.yml.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/130be1c5-5cf7-49f5-9ce0-52e319729fab)

### lambda_function.py

This is just a “Hello World” Python code deploying on lambda.

whenever I will create something to deploy in lambda I always need to do it using a “handler” function.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/8e057892-83f6-44f0-84b6-ccf8c541bbbb)

### template.yml

This is the template.yml file which will create a lambda function and a API Gateway(with only GET method) and deploy the code into the lambda function.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/cdc82ad6-7435-4b2b-b99d-43b0c4bac920)


# 5-Create Pipeline

Now let's create Pipeline

Here I am creating a pipeline and let the AWS to create a role us using this name.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/99e5542a-bc74-453e-a60e-cd1a8dfda490)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/786ac403-2326-416c-8b11-9a92505ed4fc)

### CodeCommit

I choose my Source provider AWS CodeCommit , choose the repository name and choose the branch name.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/ac780b74-f496-4b51-b154-7bda83ce65fd)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/971ce5d3-8646-439b-af5f-6c5e45f3683b)


### CodeBuild

I choose my Source provider AWS CodeBuild and in another tab creating the a build project

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/f067bbbd-5fdd-44d2-b5a5-6a26ab9522ca)

Build project

Choosing a project name here

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/52412a61-db12-4fca-8b7a-c34568423c98)

Here in the environment I am choosing, operating system as linux Runtime Standard and the latest image 5.0 and the first role created for CodeBuild.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/ebc547f5-1929-46a8-afbc-d11b3e72d479)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/2c6bbd69-fa1a-4da1-89dc-2d42b2fe48d5)

Choosing the build project created

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/dcc8c69b-3091-44c4-a1fb-bb12c88a9a17)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/835e83f4-0622-4f4d-a2c4-7f6891cdc786)

### Project successful create in pipeline

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/9dfd2fa1-c496-4cda-8d38-a562926708d7)

### Deploy stage

Here in the deployment, I am choosing AWS CloudFormation. In action mode, choosing to Create or replace a change set.

And in the BuildArtifact I am choosing — outputtemplate.yml

and in capabilities, I am choosing — “CAPABILITY_IAM”

And I am choosing the role created previously.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/333d196c-7b1f-4440-b369-0e28e5f7eada)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/f69b9281-a023-4b90-8c0c-7c8938504a8b)

PS: there was a command in buildspec, which is creating the “outputtemplate.yml” from “ template.yml”

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/ac3510d9-3a41-436a-837c-f0f36fc6eda5)


### Pipeline is created but I will edit the deploy stage

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/b17955df-f3f8-4f4f-83cd-74add7747f93)

Edit option, in the deploy stage and select the add action group.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/02fa13b2-55ca-473f-97dc-b5f1ea421c90)

in Action provider, choose CloudFormation. Input artifact, BuildArtifact. And here changeset and stack name should be the same as it was previously. 

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/38e3d0b5-c301-441d-a086-68ecec2b48d6)

The deploy stage of pipeline is comlete now. The first action group is edited to “create-changeset”

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/2245dc0f-ac13-46ff-bf0f-375ae3955916)

### Pipeline looking

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/4b8ec2e6-99b5-436d-add0-443789462a39)

### The lambda function created

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/d15dd049-3653-4005-a080-c71198afe196)

### API Gateway also attached to the lambda

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/b2e184e6-781b-483d-8169-3bb24e7aa515)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/3ca8e2fa-1109-4b4b-8d18-e1622c181110)

### The lambda code 

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/bf481136-0ca1-4173-8839-6d484cfe24ea)

### Output

let’s check the expected output 

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/26cbf088-cc4b-42b6-9942-7d9ec0b1063f)

Let test the change : all is ook

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/300d6284-3b23-46bf-b784-e9f9bfdafc16)




















































