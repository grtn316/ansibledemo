# Using Ansible and Docker Together

## Step 1: Install Ansible (https://www.redhat.com/en/technologies/management/ansible)

Install using this command: `sudo apt install ansible`

Verify that ansible is now installed: `ansible --version`

## Step 2: Install Docker

```
sudo apt update

sudo apt install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

sudo apt install docker-ce

sudo apt install docker-compose

```

## Step 3: Create a web server using a dockerfile

Create a file named: `webserver.dockerfile` using `nano` (or use the file in this repo)

and add these commands to it:

```
FROM ubuntu 
RUN apt-get update 
RUN apt-get install –y apache2 
RUN apt-get install –y apache2-utils 
RUN apt-get clean 
EXPOSE 80
CMD [“apache2ctl”, “-D”, “FOREGROUND”]
```

This will build an image using Ubuntu as the base and installing the essentials to deploy an apache web server.

Once this file is created, we will use ansible to build the image and deploy it onto your machine.

!NOTE: You can do this without ansible but this is a single example of how you could use ansible to automate a task.

## Step 4: Build and Deploy your image with Ansible

Run the following command:
```
ansible-playbook builddocker.yaml
```