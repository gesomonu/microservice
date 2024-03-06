# DevSecOps CI/CD Pipeline Project Automation Arch
![ProjectArch](https://github.com/awanmbandi/realworld-microservice-project/blob/zdocs/images/DevSecOps%20Projects%20-%20DevSecOps-P1%20(2).png)

## Continuous Observability (Monitoring & Logging) Arch
![PromGrafEFKArch](https://github.com/awanmbandi/realworld-microservice-project/blob/zdocs/images/prom-graf-efk.avif)

###### Project ToolBox 🧰
- [Git](https://git-scm.com/) Git will be used to manage our application source code.
- [Github](https://github.com/) Github is a free and open source distributed VCS designed to handle everything from small to very large projects with speed and efficiency
- [Jenkins](https://www.jenkins.io/) Jenkins is an open source automation CI tool which enables developers around the world to reliably build, test, and deploy their software
- [NPM](https://www.npmjs.com/) npm is the world's largest software registry. Open source developers from every continent use npm to share and borrow packages, and many organizations use npm to manage private development as well.
- [SonarQube|SAST](https://docs.sonarqube.org/) SonarQube Catches bugs and vulnerabilities in your app, with thousands of automated Static Code Analysis rules.
- [OWASP|SCA](https://owasp.org/www-project-dependency-check/) Dependency-Check is a Software Composition Analysis (SCA) tool that attempts to detect publicly disclosed vulnerabilities contained within a project’s dependencies.
- [Trivy|SAST|IAST](https://trivy.dev/) Trivy is the most popular open source security scanner, reliable, fast, and easy to use. Use Trivy to find vulnerabilities & IaC misconfigurations, SBOM discovery, Cloud scanning, Kubernetes security risks,and more.
- [GitGuardian|HoneyTokens](https://www.gitguardian.com/) GitGuardian helps developers and organizations secure their software development process by automatically detecting secrets like API keys, passwords, certificates, encryption keys and other sensitive data. It can as well remediate the risk for private or public source code repositories. 
- [Docker](https://www.docker.com/) Docker helps developers build, share, run, and verify applications anywhere — without tedious environment configuration or management.
- [Kubernetes](https://kubernetes.io/) Kubernetes, also known as K8s, is an open-source system for automating and orchestrating deployment, scaling, and management of containerized applications.
- [EC2](https://aws.amazon.com/ec2/) EC2 allows users to rent virtual computers (EC2) to run their own workloads and applications.
- [Fluentd|Logstash](https://www.elastic.co/logstash/) Fluentd and Logstash are a free and open server-side data processing pipeline that ingests data from a multitude of sources, transforms it, and then sends it to your favorite "stash."
- [Elasticsearch](https://www.elastic.co/elasticsearch/) Elasticsearch is a search engine based on the Lucene library. It provides a distributed, multitenant-capable full-text search engine with an HTTP web interface and schema-free JSON documents.
- [Kibana](https://www.elastic.co/kibana/) Kibana is a source-available data visualization dashboard software for Elasticsearch.
- [Prometheus](https://prometheus.io/) Prometheus is a free software application used for event/metric monitoring and alerting for both application and infrastructure.
- [Grafana](https://grafana.com/) Grafana is a multi-platform open source analytics and interactive visualization web application. It provides charts, graphs, and alerts for the web when connected to supported data sources.
- [Slack](https://slack.com/) Slack is a communication platform designed for collaboration which can be leveraged to build and develop a very robust DevOps culture. Will be used for Continuous feedback loop.

# Jenkins Complete CI/CD Pipeline Project Runbook
1) Create a GitHub Repository with the name `DevSecOps-Realworld-CICD-Project` and push the code in this branch(main) to 
    your remote repository (your newly created repository). 
    - Go to GitHub: https://github.com
    - Login to `Your GitHub Account`
    - Create a Repository called `DevSecOps-Realworld-CICD-Project`
    - Clone the Repository in the `Repository` directory/folder on your `local machine`
    - Download the code in in this repository `"Main branch"`: https://github.com/awanmbandi/realworld-microservice-project.git
    - `Unzip` the `code/zipped file`
    - `Copy` and `Paste` everything `from the zipped file` into the `repository you cloned` in your local
    - Open your `Terminal`
        - Add the code to git, commit and push it to your upstream branch "main or master"
        - Add the changes: `git add -A`
        - Commit changes: `git commit -m "adding project source code"`
        - Push to GitHub: `git push`
    - Confirm that the code is now available on GitHub

2) Sign Up For GitGuardian for continuous Secrete scanning
- Click on the following link to access GitGuardian: https://www.gitguardian.com/
    - Click on `Start For Free`
    - Select `Sign up with GitHub`
    - Once you sign up, you should have a page that looks like this...
    ![GitGuardian!](https://github.com/awanmbandi/realworld-microservice-project/blob/zdocs/images/ererere.png)

3) Create An IAM Profile/Role For The Ansible Automation Engine (Dynamic Inventory)
- Create an EC2 Service Role in IAM with AmazonEC2FullAccess Privilege 
- Navigate to IAM
![IAM!](https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/zdocs/images/Screen%20Shot%202023-10-03%20at%206.20.44%20PM.png)
    - Click on `Roles`
    - Click on `Create Role`
    - Select `Service Role`
    - Use Case: Select `EC2`
    - Click on `Next` 
    - Attach Policy: `AmazonEC2FullAccess`
    - Click `Next` 
    - Role Name: `AWS-EC2FullAccess-Role`
    - Click `Create`

4) Jenkins CI
    - Create a Jenkins VM instance 
    - Name: `Jenkins-CI`
    - AMI: `Ubuntu 22.04`
    - Instance type: `t2.large`
    - Key pair: `Select` or `create a new keypair`
    - Security Group (Edit/Open): `All Traffic` to `0.0.0.0/0`
        - What we actually need: `80`, `8080`, `9100`, `3000`, `9090`, `9000` and `22` to `0.0.0.0/0`
    - Storage: Increase to `50 GB`
    - IAM instance profile: Select the `AWS-EC2FullAccess-Role`
    - User data (Copy the following user data): https://github.com/awanmbandi/realworld-microservice-project/blob/dev-sec-ops-cicd-pipeline-project-one/installations.sh
    - Launch Instance

##### 4A) Verify the Following Services are running in the Jenkins Instance
- SSH into the `Jenkins-CI` server
    - Run the following commands and confirm that the `services` are all `Running`
```bash
# Confirm Java version
sudo /usr/bin/java --version

# Confirm that Jenkins is running
sudo systemctl status jenkins

# Confirm that docker is running
sudo systemctl status docker

# Confirm that Trivy is running
sudo systemctl status trivy

# Confirm that Terraform is running
terraform version

# Confirm that the Kubectl utility is running 
kubectl version --client

# Confirm that AWS CLI is running
aws --version
```
