# ReadMe

### Steps to configure and build checkbox.io and iTrust application:  

- Clone the github repository using `git clone https://github.ncsu.edu/cmachan/CSC519_SPRING2018PROJECT.git` command. 
- cd into CSC519_SPRING2018PROJECT directory using `cd CSC519_SPRING2018PROJECT`   
- Edit the [id_rsa](./roles/SetupJenkins/tasks/id_rsa) file present in the `roles/SetupJenkins/tasks` folder with your gitHub private ssh key
- Change the Hostname and host parameters of the [ssh_config.j2](./roles/SetupJenkins/templates/ssh_config.j2) template file in `Milestone1/roles/SetupJenkins/templates` folder with your Github credentials
```
# templates/ssh_config.j2

{{ ansible_managed | comment }}

Host https://<your_unity_id>@github.ncsu.edu
    HostName <unity_id>
    IdentityFile .ssh/id_rsa
    ForwardAgent yes
    IdentitiesOnly yes
```
- Edit the [credentials.ini](credentials.ini) with your mongo, mysql and aws credentials
- Also make sure you copy the [config](config) file inside the ~/.ssh/ folder of your ansible server machine. (location :`~/.ssh/config`). 
- Run the playbook on your Ansible server using the following command:
```
ansible-playbook -i inventory main.yml
```
- Go to the AWS EC2 Console to get the IP address of the Jenkins server (with instance name: `ec2_m1`)
- Open the web browser and type: `http://<jenkins-server-ip-address>:8080`. This will open up a webpage showing that the two builds for checkbox.io and iTrust were successful.
- Note down the public IP address of the iTrust server and checkbox server --> `AWS console` will show the IP address of the iTrust and checkbox server. Instance with name `ec2_checkbox` gives the IP address of checkbox VM and the one with name `ec2_iTrust` gives the IP address of the iTrust VM.
- Open the web browser and type: `http://<ip addr of iTrust>:8080/iTrust2` to open up the iTrust web page
- Open the web browser and type: `http://<ip addr of checkbox>` to open up the checkbox web page

### Milestone learning experience 
The overall learning experience for provisioning and configuring applications using ansible and Jenkins can be found [here](./issues.md) 

### Screencast Link 
[Screencast](https://youtu.be/ZCB7ady9PdM)


