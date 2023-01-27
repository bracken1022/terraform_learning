
# docker example

This is a basic terraform example.

Create a directory named learn-terraform-docker-container

    mkdir learn-terraform-docker-container

Navigate into the working directory.

    cd learn-terraform-docker-container

Create a file called `main.tf` and paste the following configuration:

    terraform {
        required_providers {
            docker = {
            source  = "kreuzwerker/docker"
            version = "~> 2.13.0"
            }
        }
    }
    
    provider "docker" {}
    
    resource "docker_image" "nginx" {
        name         = "nginx:latest"
        keep_locally = false
    }
    
    resource "docker_container" "nginx" {
    image = docker_image.nginx.latest
    name  = "tutorial"
        ports {
            internal = 80
            external = 8000
        }
    }


Initialize the project, which downloads a plugin called a provider that lets Terraform interact with Docker.

    terraform init


Provision the NGINX server container with apply. When Terraform asks you to confirm type yes and press ENTER.

    terraform apply

