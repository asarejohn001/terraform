# How I used Docker and Terraform to provision the NGIX server in minutes.

## Check out [all the screenshot](TerraformDockerImages). 

## Steps
1. I downloaded and installed the [Docker application](https://docs.docker.com/desktop/install/mac-install/) for Mac
2. Use Terminal and bash/Linux language to open Docker
   ```
    open -a Docker
   ```
3. Created a directory and navigated to it to create a terraform file
   ```
   mkdir learn-terraform-docker-container
   cd learn-terraform-docker-container
   touch main.tf
   ```
4. Inside the main.tf file, I wrote the Terraform configuration.
   ```
   terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.1"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name         = "nginx"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "tutorial"

  ports {
    internal = 80
    external = 8000
  }
}
```
