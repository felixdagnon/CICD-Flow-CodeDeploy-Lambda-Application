# CICD Pipeline using AWS DevOps (Cloud9, CodeCommit, CodeBuild, S3, CloudFormation(SAM), Lambda, API Gateway)

Here I create CICD pipeline flow  for a serverless application. It's works in my environment.

(Always create an IAM user, and add policies according to your need. Never use root account).

Follow Best Practices for Cloud Security with AWS IAM: Managing Groups, Policies, and Roles



![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/19d85248-91dd-4967-8b06-7152609ce845)

## CodeBuild

## Create Iam role for CodeBuild

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/52368426-13b8-4101-9ffd-20346792107f)

## Create role for CodeDeploy use cloudformation for policies with AWSLambdaExecute permission and add inline policy

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/4595b200-bc15-4cdf-a0c6-a6c3755a4040)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/41736a78-569f-49be-a909-f36495651315)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/019c1e85-1d81-4a72-a953-9afae736250f)

## Create S3 bucket for CodePipeline

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/39a3c393-ad68-4345-84ec-c87972f88129)


## Create CodCommit Repo and put the staff in

let's create a CodeCommit repository first and push our code from Cloud9 IDE.

I will store all code in CodeCommit repository.

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/802323ca-7154-4340-9907-587719e89065)

Clone the repo in Cloud9 and upload files.

I use git commands (git add -A,  git commit -m "Add sample application file", git push)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/9dc84819-cfcb-48b7-aeb7-194a8783fde7)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/b0f0d02d-195b-48cc-9bf5-fda79473b1c5)


![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/936342c3-aad5-43f8-81ea-664e27e3c411)


## Create Pipeline

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/99e5542a-bc74-453e-a60e-cd1a8dfda490)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/786ac403-2326-416c-8b11-9a92505ed4fc)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/ac780b74-f496-4b51-b154-7bda83ce65fd)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/971ce5d3-8646-439b-af5f-6c5e45f3683b)


### Create project

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/f067bbbd-5fdd-44d2-b5a5-6a26ab9522ca)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/52412a61-db12-4fca-8b7a-c34568423c98)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/ebc547f5-1929-46a8-afbc-d11b3e72d479)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/2c6bbd69-fa1a-4da1-89dc-2d42b2fe48d5)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/dcc8c69b-3091-44c4-a1fb-bb12c88a9a17)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/835e83f4-0622-4f4d-a2c4-7f6891cdc786)

### Project successful create in pipeline

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/9dfd2fa1-c496-4cda-8d38-a562926708d7)

### Deploy stage

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/333d196c-7b1f-4440-b369-0e28e5f7eada)

![image](https://github.com/felixdagnon/CICDFlow-CodeDeploy-LambdaApplication/assets/91665833/f69b9281-a023-4b90-8c0c-7c8938504a8b)

































