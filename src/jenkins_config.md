# Jenkins Configuration

As we have the build pipeline running the stages as defined in the Jenkinsfile for any project, we have a lot more going once the build is succedded. Many things are configured into the deploy staging pipeline. 

- Running the ansible playbook for testing. 
- Sending the build status notification to Samagra discord server.

Jenkins allow us to configure all such tasks.

![image](https://user-images.githubusercontent.com/79367883/222879979-6b7b21b9-438b-40db-b24a-a4c0c7efa151.png)

1. Creating build tags as string parameters.

![image](https://user-images.githubusercontent.com/79367883/222880060-ec3e0d5b-0f6c-450c-a389-f218af683d3d.png)

2. Running Shell commands after each build runs. 

![image](https://user-images.githubusercontent.com/79367883/222880192-79ba4f55-2f6c-4161-99d9-283a5dab9f9b.png)

Here as you can see, the tag parameter which we created in step 1 gets used with ansible-playbook. You can create several parameters if needed.

3. Setting up discord notifier using webhook URL.

![image](https://user-images.githubusercontent.com/79367883/222880245-f4a047de-6e4b-49d6-950a-dc298fb675ec.png)'

---

If need arises, you can manually deploy the projects using the *build with parameters* option.

![image](https://user-images.githubusercontent.com/79367883/222880709-e897de61-2315-4504-a6e1-3fdf389f5efd.png)


