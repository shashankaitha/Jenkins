# **Jenkins Installations (Master and Slave)**

Jenkins Pre-Req:
    Install below applications to setup master and slave architecure

## _1. Install Java 11_


    sudo su

    apt update && apt install -y openjdk-11-jdk


## _2. Install Maven:_

    apt install -y maven


## _3. Install unzip and net-tools:_

    apt install -y jq unzip net-tools


## _4. Install Terraform:_

    cd /usr/local/bin

    wget https://releases.hashicorp.com/terraform/1.7.1/terraform_1.7.1_linux_amd64.zip

## _5. Install Packer:_

    wget https://releases.hashicorp.com/packer/1.10.0/packer_1.10.0_linux_amd64.zip

##  _6. Create ansible user:_

    sudo useradd -m ansibleadmin --shell /bin/bash \
    && sudo mkdir -p /home/ansibleadmin/.ssh \
    && sudo chown -R ansibleadmin /home/ansibleadmin/ \
    && sudo usermod -aG sudo ansibleadmin \
    && echo 'ansibleadmin ALL=(ALL) NOPASSWD: ALL' | sudo tee -a /etc/sudoers

    cp /home/ubuntu/.ssh/authorized_keys /home/ansibleadmin/.ssh/authorized_keys

    cat /home/ansibleadmin/.ssh/authorized_keys

## _7. Install Ansible:_

    sudo apt install software-properties-common -y
    sudo apt-add-repository --yes --update ppa:ansible/ansible
    apt update && sudo apt install ansible -y

    Note: Once the installation is completed disable the host_key_selection and add remote user as ansible

    remote_user=ansibleadmin
    private_key_file=/home/ansibleadmin/ansbileadmin.pem
    host_key_checking=False

## _8. Install Docker and give Access:_
    curl https://get.docker.com | bash

    usermod -a -G docker ubuntu & usermod -a -G docker ansibleadmin

## _9. Install Aws_Cli:_

    https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

## _10. Install TrivyScanner:_

    wget https://github.com/aquasecurity/trivy/releases/download/v0.41.0/trivy_0.41.0_Linux-64bit.tar.gz

    tar xzvf trivy_0.41.0_Linux-64bit.tar.gz

    trivy version

Take an Image from the instances and use it for slave groups.

## _11. Install Jenkins Version 2.401.2:_

Artical: https://directdevops.blog/2019/01/04/installing-specific-lts-version-of-jenkins-on-ubuntu/

    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null

    apt-get update

    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys <KEyNumber>

    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 5BA31D57EF5975CA

    apt-get update

    sudo apt-cache madison jenkins

    sudo apt-cache madison jenkins | grep -i 2.401.2

    sudo apt-get install jenkins=2.401.2 -y

    Default port: 8080


## _12.Install Plugins in Jenkins:_

1. AWS steps
2. DockerVersion 1.5
3. SonarQube Scanner
4. Blue Ocean
5. MultiBranch  Scan Webhook Trigger
6. Slack Notification
7. Ansible

