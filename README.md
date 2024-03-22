# hello-World App Deployment

## The steps to build and run the Docker container locally.
1. Clone this repository: `git clone https://github.com/AmbitiousSam/hello-wprld.git`
2. Run the following docker commands to build and run the Docker container
```
docker build -t hello-world:latest
docker run -p 8080:80 hello-world:latest
```

## How the CI/CD pipeline works and how to trigger it.
The workflow CI/CD pipeline contains the following
1. First the pipeline checkouts the latest code from the branch that is set in our case its the main branch.
2. Then it sets/log in to the aws account using the aws keys set in the github secrets.
3. Then we log in to the AWS ECR to be able to push the docker image.
4. Next step is to build the docker image and push it to the repository.
5. We fill the task definition with the container image:tag that was pushed to ECR repository
5. Finally the amazon-ecs-deploy-task-definition action helps us to deploy our docker image to the  Amazon ECS service. It will update or create the service.

## How to run the deployment script or commands to deploy the container to the chosen cloud service.
1. The pipeline handles the deployment of the container to AWS ECS service.
2. To manually update the deployment we can use the following aws cli command:
```
aws ecs update-service --cluster helloworld --service-name sample-app --task-definition <TasDefinitionARN>
```
3. This should update the service with the latest task revision and container.
