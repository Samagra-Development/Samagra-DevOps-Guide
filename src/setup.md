# Setup of DevOps pipeline

DevOps pipeline has the following main components. 

1. Jenkins Server
2. Hashicorp Vault
3. Docker Swarm (This could be your localhost as well)
4. Database Server (This could be your localhost as well, same as Docker Swarm)
5. Private Docker Registry
6. Ansible
7. Preferred OS environment is Linux, Setup is not tested on windows

Setup
-------
- Install [Jenkins](https://www.jenkins.io/doc/book/installing/)
- Setup Hashicorp [Vault](https://developer.hashicorp.com/vault/tutorials/getting-started/getting-started-deploy) 
  - Generate Unseal keys and vault token
- Install [Docker](https://docs.docker.com/engine/install/ubuntu/) 
- Initialize [Docker Swarm](https://docs.docker.com/engine/reference/commandline/swarm_init/) 
  - Docker swarm needs an external [overlay network](https://docs.docker.com/network/overlay/) to be created. Create a network named `application_default` in Docker         
- [Install ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) on Docker Swarm and Database servers
- Setup Docker Registry
  - Use the following compose for private registry setup. 
  ```
  version: '3'

  services:
    registry:
      image: registry:2
      ports:
      - "[Replace this with private_ip or nothing]:5000:5000"
      environment:
        REGISTRY_STORAGE_FILESYSTEM_ROOTDIRECTORY: /data
      volumes:
        - ./data:/data
  ```
  
Configure
----------
- **Configure Jenkins**
  - Setup Pipelines  
    - Go to `/home` location and clone the `<project>-devops` pipelines. For example, go to `/home` and clone `https://github.com/Unified-Learner-Passbook/ULP-devops`
    - Create symbolic links to Jenkins jobs `ln -s /home/ulp-devops/jobs/ULP /var/lib/jenkins/jobs/`
    - Set permissions `chown -R jenkins:jenkins jobs && chown -R jenkins:jenkins /var/lib/jenkins`
    - Restart Jenkins - `systemctl restart jenkins`. You should be able to see all the Jobs on the Jenkins Dashboard. 
  - Setup environment variables in Jenkins
    - Go to **Dashboard -> Manage Jenkins -> Configure System**
    - Select environment variables checkbox and add `VAULT_ADDR_DEV` and `VAULT_TOKEN_DEV` with corresponding values you got while setting up Hashicorp Vault
    - These variables are needed in the `deploy` jobs in the pipeline. 

- **Configure Ansible**
  - `jenkins` user should be able to `ssh` on to the Docker Swarm and Database Servers 
    - Switch to `jenkins` user and run `ssh-keygen`. Select all default options. 
    - Copy public key from `~/.ssh/id_rsa.pub` and paste it under `~/.ssh/authorized_keys` on the Docker Swarm and Database Server
  - Configure Ansible Hosts
    - Go to `https://github.com/Unified-Learner-Passbook/ULP-devops/blob/master/ansible_workspace_dir/inventory/hosts`  
    - Uncomment the localhost lines or add `localhost` under `dev` group. You can read more about ansible hosts [here](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html) 

  
  
