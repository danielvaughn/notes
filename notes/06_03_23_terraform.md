# 06_03_23

Terraform is a technology for managing infrastructure as code.
You use declarative configuration files to describes the end state of your system, and Terraform handles the rest.

## When not to use Terraform

- Small-scale deployments
- Non-cloud environments
- Complex orchestrations (use k8s or something)
- Software configuration (use ansible)
- Frequent real-time changes
- Proprietary cloud services
- State management

---

## Immutability

It leverages the concept of "immutable infrastructure".

Traditionally, when you want to create infrastructure, you do one of two things:

1. Log into a cloud provider such as AWS or GCP and use their UI to create it
2. Use an automation tool like Ansible to create it for you

In both of these scenarios, you run into trouble if/when you need to change your infrastructure.
What happens if something goes wrong during the upgrade, like a network failure?
You'd be stuck in an undefined "version 1.5", making it very difficult to finish the upgrade.

Terraform's approach treats infrastructure like immutable objects,
instead choosing to create a new instance of the infra,
and only moving traffic over once the new instance has been created.

This provides several benefits, but comes with the tradeoff that the infrastructure should not be stateful.

---

## Setup

Within configuration files, you write things called "modules",
which are configurable collections of resources.

Terraform generates a "plan", prompting you for approval before making changes.
It also maintains a "state" file which acts as a source of truth for your environment.

**QUESTION**: what happens _when_ the environment invariably drifts from the state file?

Terraform configuration files are made up of blocks.

A "terraform" block defines the overall settings for terraform:

```tf
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.1"
    }
  }
}
```

In the above code, we defined the dependencies for the project.

There are also "resource" blocks which define resources:

```tf
resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "tutorial"
  ports {
    internal = 80
    external = 8080
  }
}
```

The above code defines a docker container with nginx, mapping port 80 to the host machine port 8080.

---

## Running

After initially writing your configuration file,
you have to run the equivalent of `npm install`.
The command is `terraform init`.
This command does some initial setup and installs the necessary providers.

Once the project is initialized,
you can run `terraform plan` to find out what terraform will do.

You can also run `terraform fmt` to format your files and `terraform validate` to validate your files.

Finally, run `terraform apply` to execute the plan.

**QUESTION**: obviously the apply does a lot of stuff, how do I run verbose?

Once the plan has been executed, run `terraform show` to inspect the state.

To destroy your infastructure, run `terraform destroy`.
