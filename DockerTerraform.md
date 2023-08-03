# How I used Docker and Terraform to provision the NGIX server in minutes.
At the end of this project, I familiarized myself with Terraform and showcased my Linux skills.

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
5. I initiated he project, which downloads a plugin called a provider that lets Terraform interact with Docker and then provision the NGINX server container with the Terraform command "apply"
```
terraform init
terraform apply
```
