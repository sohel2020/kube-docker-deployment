# Docker Container build and deploy into kubernetes cluster using ansible.

### Prerequisite
1. ansible 

###Deployment steps:
**step-1:** Install ansible and git in your local ubuntu machine:-
```bash
$ sudo apt-add-repository -y ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install -y ansible git
```

**step-2:** Run ssh agent
```bash
$ eval $(ssh-agent -s)
```
**step-3:**  Add your ssh key (which you are using to login into the cluster)
```bash
$ ssh-add devops-key.pem
```
**step-4:** Navigate to your project directory
**step-5:** Add  your cluster IP address inside **hosts** file. Just below the [docker-build] section. 
**step-6:** Then run 
```bash
$ ansible-playbook -i hosts playbook.yml
```
It will ask a docker images version number. Please input it (Example: v1) and also ask kubeclt action name. (if your pod defination is already created inside your cluster then just press enter key so it'll pick **update** as a default value. If this is your first time that your are going to register your pod defination, then just type **create** , so your pod defination will be created for you in your kubernetes cluster)

After then it'll install all dependency , clone your code from github, build docker images , push it to docker hub and then run kubeclt to deploy new images into the cluster.

