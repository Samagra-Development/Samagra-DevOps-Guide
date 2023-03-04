# Jenkins

## Dashboard
It is the main Jenkins screen which you would be able to see just after login. 

![image](https://user-images.githubusercontent.com/79367883/222869591-78f431ed-f69c-4fc0-87bb-877abb4dbbe0.png)


## Project Space
In project space there are directories for specific projects or job.

![image](https://user-images.githubusercontent.com/79367883/222869626-73a24e17-62c8-4ab4-a2bf-de08e804fa38.png)

## Pipelines
For each job we have two pipelines.
- build
- deploy-staging
- deploy-prod (third pipeline yet to come)
![image](https://user-images.githubusercontent.com/79367883/222869689-285557b2-cb88-491b-8e66-2828d29fb8a4.png)

#### Build Pipeline

This is a **multibranch pipeline** and it can make Docker image builds of all branches and new PRs that are created. Images are tagged by *branch name* or *PR-(Number)* and pushed to a private docker registry.

![image](https://user-images.githubusercontent.com/79367883/222869924-9e602ead-cefd-43b8-861e-9d309b779233.png)

#### Deploy-staging Pipeline

Whenever commits are made to main/master branch, this job automatically deploys the code to the server and pushes a notification on the discord channel regarding the success and failure of the jobs. 
![image](https://user-images.githubusercontent.com/79367883/222870231-34fa2fc2-7cc5-4162-bf6c-60c662073bc9.png)

#### Deploy-prod
This pipeline will be used to deploy to the prod server and will be manually used to deploy the changes
![image](https://user-images.githubusercontent.com/79367883/222870334-3308af3d-b1c8-40b1-a926-34d25ba40e16.png)

