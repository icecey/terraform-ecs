## Deploy application in ECS Fargate

- We will be able to run one command to deploy our entire application giving us:

  - A Virtual Private Cloud with private and public subnets
  - Internet Gateway and NatGateway
  - Multiple running container instances
  - A load balancer distributing traffic between the containers
  - Auto scaling of your resources
  - Health checks and logs

To get internet traffic to containers using a load balancer, the load balancer is placed into a public subnet. ECS configures the load balancer to forward traffic to the container tasks in the private subnet:
![alt text](https://github.com/CarlosPalaciosC/terraform-ecs/blob/master/networking.png?raw=true "Deployments")

- All configurations can be changed in:

```shell
variables.ft
```

You can choose your docker image application to deploy in Fargate, changing `app_image` and `app_port` in `variables.tf`

```shell
variable "az_count" {
  description = "Number of AZs to cover in a given region"
  default     = "2"
}

variable "app_image" {
  description = "Docker image to run in the ECS cluster"
  default     = "gcr.io/google-samples/hello-app:2.0"
}
```

1- Terraform init, plan and validate scripts

```shell
terraform init
terraform plan
```

```shell
terraform validate
```

2. Apply changes

```shell
terraform apply
```

Output console: `Plan: 34 to add, 0 to change, 0 to destroy.`

Before to create all resources you can access to application with

```
curl -v http:/<LOAD_BALANCER_HOSTNAME>/
```

3. Remember to destroy all resources to avoid incurring payments

```shell
terraform destroy -auto-approve
```
