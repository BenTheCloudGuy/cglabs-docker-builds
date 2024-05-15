# Custom DevContainer Image Build

This Repo contains the dockerfile used for building a devcontainer for CodeSpaces and local Dev workflows and mirrors the same tools found in the Github Runner Build so we can develop using the same stack/tools we will use for build/release in GH Actions. 

Docker Image can be found at: [DockerHub | BenTheBuilder/gh-runner-devcontainer](https://hub.docker.com/r/benthebuilder/cglabs-gh-runner-devcontainer)

## Features

- **Customizable**: Easily configure the runner to suit your specific needs and environment.
- **Docker-based**: Utilizes Docker to encapsulate the runner environment, ensuring consistency and portability.
- **Scalable**: Can be scaled horizontally by spinning up multiple instances to handle parallel jobs.
- **Self-hosted**: Enables you to run workflows on your own servers or cloud infrastructure.
- **Flexible**: Supports running workflows for both public and private repositories.

## Installed Applications

- Ansible
- Hashicorp Packer
- Hashicorp Terraform
- Azure CLI
- Powershell Core
   - Az Module
   - AzureAD Module
   - Microsoft.Graph Module


## Prerequisites

Before using this Docker image, ensure you have the following prerequisites installed:

- Docker Engine: [Installation Guide](https://docs.docker.com/get-docker/)
- GitHub Repository: Set up a repository on GitHub where you want to use the custom runner.

## Usage

### 1. Pull the Docker Image

Pull the latest version of the custom GitHub Runner Docker image from Docker Hub:

```bash
docker pull benthebuilder/cglabs-gh-runner
```

### 2. Configure Runner

Set up the runner by providing necessary configuration options such as GitHub registration token, runner name, etc. These configurations are typically provided through environment variables.

### 3. Run Docker Container

Start the Docker container using the pulled image:

```bash
docker run -d --name='gh-runner-devcontainer:latest' `
```

## Configuration

You can configure the custom GitHub Runner by providing environment variables to the Docker container. Refer to the [GitHub Actions documentation](https://docs.github.com/en/actions/hosting-your-own-runners/about-self-hosted-runners#self-hosted-runner-groups) for a list of available configuration options.

## License

This project is licensed under the [MIT License](LICENSE).