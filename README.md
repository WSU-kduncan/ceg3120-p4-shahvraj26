# CEG3120 Final Project Write-up

## Project Overview/Checklist:

### Milestone 1:
- [x] Created Public Repository
- [x] Cloned Repo to local machine
- [x] Dockerized my website using 127.0.0.1:5000 and index.html file 
### Milestone 2:
- [x] Downloaded the aws command line
- [x] Created an ECR Repository
- [x] Setup a workflow in github
- [x] Tested it with a Reference tag

## Installation/Setup Requirements:
- [x] Install Docker - [Click Here for Installation Link](https://www.docker.com/products/docker-desktop)
- [x] Install AWS CLI - [Click Here for Installation Link](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html)
- [x] Install WSL2 - [Click Here for Installation Link](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

## Milestone 1 Overview:

### Step 1:
- Setup and Clone the public repository from Pilot!
	- Create a new ssh key on your local machine
	- Add the public key to github
	- On your local machine clone the created public repository using the `ssh` tab 
### Step 2:
- Setup a Docker Repository!
	- Go to the Docker App. Create a Get-Started Image by copying the command given.
	- Type `docker ps` to see the container in action
	- Kill the container by typing `docker kill [name]'
	- Create a New Docker Repository with the httpd:2.4 installed.
	- The command is `docker pull httpd:2.4`
	- Build the webserver in your repository:
		- `docker build -t [name of image] .` : This builds the image in the directory `.` specified
		- `docker run -d -p 5000:80 [name of image]` : This runs the image on the local machine with port 80 binded to it. 
### Step 3:
- Build a Docker Repository with your own index.html!
	- Create a html directory in your public repo
		- Inside the html file create an index.html file and add some content.
	- Create a Docker file named `Dockerfile` exactly inside your public repo.
	- Add the following lines to the file:
		- `FROM httpd:2.4` : This pulls the apache2 things
		- `COPY ./html/ /usr/local/apache2/htdocs/` : This line copies the index.html file from .html and put it  into apache2 for Docker to use  it.
	- Save the Dockerfile
### Proof of Milestone 1:
- Go to [127.0.0.1:5000](http://127.0.0.1:5000/)

![Proof](ProofOfDocker.png)

# Milestone 2 Overview:

### Step 1:
- Download AWS CLI V2 on your WSL2 Machine
- Commands to download and Install:
	- `curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"`
	- `unzip awscliv2.zip`
	- `sudo ./aws/install` : Installs aws on $PATH

### Step 2:
- Configure your AWS with the Credentials.
- `aws configure` : This allows you to autmatically add your keys.
	- Keys should be kept private and can be found on Pilot.

### Step 3:
- After configuring the AWS IAM, you can create the image. 
- Type the command `aws create-repository --repository-name [name of repo] --region [region of your aws]
	- This will create your repository in aws with those credentials.

### Step 4:
- Create a workflow!
- In your github repo create a secret directory named `.github`
- Inside the .github dir create another directory named `workflows` 
- Inside the workflows dir you want a yaml file that specifies a workflow that deploys to Amazon AWS. 
	- A link to the [AWS yaml file guide](https://docs.github.com/en/actions/guides/deploying-to-amazon-elastic-container-service)
- When creating the yaml file make sure to add your region specified when you created your repository in the `AWS_REGION` line.
- Make sure to add the repository name (Exactly) in the `ECR_REPOSITORY` line.
 
### Step 5:
- Add the secret keys to Github secrets!
	- Because it is a public repo, we can't add secret keys to the repo itself, so we need to use githubs secret tool,w hich allows us to add private keys into public repo's
- Go to your public repo
- Go to Settings
- Go to Secrets, and add your AWS SECRET KEY and AWS ACCESS Key.
	- Make sure its the same as the one you used to configure your aws cli.

### Step 6:
- Last step is to have the workflow deploy. 
	- In our yaml file we specified that when a release is made, make sure to start the workflow.
- To start a release go to your public repo, and on the side there will be something called `Releases`
- Click on Create new release, and follow the directions specified. 
- After creating it, go to the `Actions` tab to see your workflow being deployed!

### Proof of Workflow:
[Workflow](workflow.png)
### Proof of YAML File:
[Yaml File](yamlfile.png)


# End of Project
Hope you learned the necessary tools of a github project with docker, workflows, etc.
