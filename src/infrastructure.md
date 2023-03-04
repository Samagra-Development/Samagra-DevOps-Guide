# Infrastructure Overview

![image](https://user-images.githubusercontent.com/79367883/222868082-35a5e06a-00ba-46e0-abb6-ff2369ae0525.png)

1. `Development` : Developers work on code changes locally and push their changes to a GitHub repository.

2. `GitHub Actions` : When a code change is pushed to GitHub, a GitHub Action is triggered to run automated tests on the code. This ensures that any issues are caught early and can be fixed before they are deployed.

3. `GitHub Webhooks` : Once the code is merged, GitHub webhooks trigger a Jenkins job to build and deploy the code changes to a staging environment.

4. `Jenkins` : Jenkins runs a build pipeline to verify the build.

5. `Deploy` : Jenkins has another pipeline (deploy-staging) which deploy the code changes to the production environment using Ansible playbooks.

6. `Hashicorp Vault`: It can be used to manage secrets that are required by the various tools and processes involved in the pipeline. Ansible fetches these secrets from here. 