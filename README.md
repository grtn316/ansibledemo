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

Create an `index.html` file in your directory and put some `hello world` text in the file.

Create a file named: `Dockerfile` using `nano` (or use the file in this repo)

and add these commands to it:

```
FROM nginx
COPY index.html /usr/share/nginx/html/index.html
```

This will build an image using NGINX as the base and copying your index.html file to it.

Once this file is created, we will use ansible to build the image and deploy it onto your machine.

!NOTE: You can do this without ansible but this is a single example of how you could use ansible to automate a task.

## Step 4: Build and Deploy your image with Ansible

Run the following command:
```
ansible-playbook builddocker.yaml

ansible-playbook runmyimage.yaml
```

## View your website running inside of a docker container

On your computer, navigate to `http://localhost`. If you are using a terminal, you can use the command: `curl localhost` and you should get back a response that says `Hello, This is my example website.`

## Things to review

- Docker commands
  - docker images
  - docker ps
  - docker ps -a -q
  - docker rmi
  - docker rm
  - sudo docker run -it --entrypoint /bin/bash myimage
  - docker-compose
- ansible commands
  - ansible-playbook
  - anisble
- Ansible Automation capabilities and how you can enforce state across a large quanity of servers using Automation controller or simply using it in its raw form as seen in this example.
- How docker containers are used with Kubernetes
- Kubernetes
- Look up the kinds of base images you can use for docker files.
- Review the structure / commands of a docker file
- Look closely at the `hosts` and `become` lines in the ansible `yaml` files.
- Explore how you could run ansible against other servers and configure them.
- Know what a `yaml` file is and what the letters stand for.
- Check out docker hub and browse the images
- Look up a docker registry and read and article about how you could deploy your own.
- Look up Red Hat Satellite and how it can manage docker images and packages to install on servers.
- Look at `Dockerfile.old` as another example of deploying a web server (its broken)
- Look up NGINX