# Github

## Repositories
---
- [**samagra-devops**](https://github.com/Samagra-Development/samagra-devops) : It is the main repo that contains Jenkins job and Ansible roles for services that are reproducible in other projects at Samagra.
- Each project then contains a (project-name)-DevOps repo. For example [ULP-Devops](https://github.com/Unified-Learner-Passbook/ULP-devops) etc.

<!-- Here we can also talk about where are our Jenkinsfile stored. In build/Jenkins for all the project repos and similarly for Dockerfile. -->

## Project Structure
---
For each project which we have as pipeline, In their github repository we follow a common structure for getting the Dockerfile and Jenkinsfile.

```
root-project-repo/
    ├── Dockerfile
    ├── build/       
            ├── Jenkinsfile
```

The Dockerfile needs to be tested by developers for any errors and once it is ready, we can use it to deploy the project in private docker registry on docker swarm. 

The Jenkinsfile contains all the necessary steps for several stages in a pipeline which eventually builds the project on server and deploys it.

## Webhook URLs
---
![image](https://user-images.githubusercontent.com/79367883/222879655-78aab321-5f95-4b5f-91f0-0251a16fa91c.png)

In each project, we have the webhook which triggers the events occuring on github to the jenkins which helps in detecting the changes going in a repository.
