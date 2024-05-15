FROM ubuntu:20.04

# Set the Arguments for the Dockerfile
ARG RUNNER_VERSION="2.314.1"        # Use this to set the Download Version for the Runner
ARG OS_VERSION="20.04"              # Use this to set the Download Version for the Microsoft Repo

# Prevents installdependencies.sh from prompting the user and blocking the image creation
ARG DEBIAN_FRONTEND=noninteractive

# Update apt and add docker user
RUN apt update -y && apt upgrade -y && useradd -m docker

# Install Dependencies
RUN apt install -y --no-install-recommends \
    curl jq build-essential libssl-dev libffi-dev python3 python3-venv python3-dev python3-pip software-properties-common openssh-client wget apt-transport-https curl gnupg unzip vim iputils-ping

# Install Powershell Core
RUN wget -q https://packages.microsoft.com/config/ubuntu/${OS_VERSION}/packages-microsoft-prod.deb \
    && dpkg -i packages-microsoft-prod.deb \
    && apt update -y \
    && apt install -y powershell 

# Install Azure Powershell Modules
RUN pwsh -c "Install-Module -Name Az -Force" \
    && pwsh -c "Install-Module -Name AzureAD -RequiredVersion 2.0.2.140 -Force" \
    && pwsh -c "Install-Module -Name Microsoft.Graph -Force" \
    && pwsh -c "Install-Module -Name powershell-yaml -Force"

# Install Azure Tools
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash 

# Install Terraform & Packer
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg \
    && echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list \
    && apt update \
    && apt install -y terraform packer \
    && terraform --version \
    && packer --version

# Install Ansible
RUN apt-add-repository -y --update ppa:ansible/ansible \
    && apt update -y \
    && pip3 install pywinrm pyvmomi ansible \
    && ansible --version \
    && mkdir /etc/ansible/ \
    && chown docker /etc/ansible/ \
    && chmod 755 /etc/ansible/

# set the user to "docker" 
USER docker