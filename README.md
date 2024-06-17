# Terraform AWS Directus Module

This Terraform module deploys Directus on an AWS Fargate ECS cluster.

## Features

- Easy deployment of Directus on AWS Fargate ECS
- Automatic scaling and load balancing
- Highly available and fault-tolerant architecture
- Customizable configuration options
- S3 integration for static assets

## To-Be-Done

- Implement Redis to allow multi-container deployment (currently only one is supported) (https://docs.directus.io/self-hosted/config-options.html#redis)
- Implement Amazon Cognito authentication
- HTTPS support

## Prerequisites

Before using this module, make sure you have the following prerequisites:

- AWS account
- Terraform installed
- Basic knowledge of AWS services and Terraform

## Usage

To use this module, follow these steps:

1. Clone the repository:

    ```bash
    git clone https://github.com/your-username/terraform-aws-directus.git
    ```

2. Change into the module directory:

    ```bash
    cd terraform-aws-directus/examples
    ```

3. Initialize the Terraform workspace:

    ```bash
    terraform init
    ```

4. Customize the module variables in `variables.tf` according to your requirements.

5. Deploy the Directus infrastructure:

    ```bash
    terraform apply
    ```

6. Access the Directus application using the provided URL.

## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |
| <a name="provider_random"></a> [random](#provider\_random) | n/a |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_ecs"></a> [ecs](#module\_ecs) | terraform-aws-modules/ecs/aws | 5.11.2 |

## Resources

| Name | Type |
|------|------|
| [aws_ecs_service.directus](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ecs_service) | resource |
| [aws_ecs_task_definition.directus](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ecs_task_definition) | resource |
| [aws_iam_access_key.directus](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_access_key) | resource |
| [aws_iam_policy.cloudwatch-logs-policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy) | resource |
| [aws_iam_role.ecs-service-role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role.ecs-task-role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role_policy_attachment.ecs-service-role-ecs-task-execution](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_user.directus](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user) | resource |
| [aws_iam_user_policy.lb_ro](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user_policy) | resource |
| [aws_lb.directus](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb) | resource |
| [aws_lb_listener.directus-lb-listener-http](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb_listener) | resource |
| [aws_lb_target_group.directus-lb-target-group-http](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb_target_group) | resource |
| [aws_s3_bucket.directus](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket) | resource |
| [aws_secretsmanager_secret.directus-admin-password](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/secretsmanager_secret) | resource |
| [aws_secretsmanager_secret.directus-secret](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/secretsmanager_secret) | resource |
| [aws_secretsmanager_secret.directus-serviceuser-secret](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/secretsmanager_secret) | resource |
| [aws_secretsmanager_secret_version.directus-admin-password-version](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/secretsmanager_secret_version) | resource |
| [aws_secretsmanager_secret_version.directus-secret-version](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/secretsmanager_secret_version) | resource |
| [aws_secretsmanager_secret_version.directus-serviceuser-secret-version](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/secretsmanager_secret_version) | resource |
| [aws_security_group.ecs-sg](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_security_group.lb_sg](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [random_password.directus-admin-password](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/password) | resource |
| [random_password.directus-secret](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/password) | resource |
| [aws_caller_identity.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity) | data source |
| [aws_iam_policy_document.cloudwatch-policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_iam_policy_document.s3-policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_region.current](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/region) | data source |
| [aws_s3_bucket.directus](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/s3_bucket) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_additional_configuration"></a> [additional\_configuration](#input\_additional\_configuration) | Additional configuration to apply to the Directus container | `map(string)` | `{}` | no |
| <a name="input_admin_email"></a> [admin\_email](#input\_admin\_email) | The email address of the admin user | `string` | n/a | yes |
| <a name="input_admin_password"></a> [admin\_password](#input\_admin\_password) | The password of the admin user (if empty, it will be generated automatically) | `string` | `""` | no |
| <a name="input_application_name"></a> [application\_name](#input\_application\_name) | The name of the application | `string` | n/a | yes |
| <a name="input_cloudwatch_logs_stream_prefix"></a> [cloudwatch\_logs\_stream\_prefix](#input\_cloudwatch\_logs\_stream\_prefix) | The prefix of the CloudWatch Logs stream | `string` | `"directus"` | no |
| <a name="input_cpu"></a> [cpu](#input\_cpu) | The number of CPU units to reserve for the Directus service | `number` | `2048` | no |
| <a name="input_create_cloudwatch_logs_group"></a> [create\_cloudwatch\_logs\_group](#input\_create\_cloudwatch\_logs\_group) | Whether to create a CloudWatch Logs group | `bool` | `false` | no |
| <a name="input_create_s3_bucket"></a> [create\_s3\_bucket](#input\_create\_s3\_bucket) | Whether to create an S3 bucket | `bool` | `false` | no |
| <a name="input_healthcheck_path"></a> [healthcheck\_path](#input\_healthcheck\_path) | The path of the healthcheck endpoint | `string` | `"/server/ping"` | no |
| <a name="input_image_tag"></a> [image\_tag](#input\_image\_tag) | The tag of the Docker image | `string` | `"latest"` | no |
| <a name="input_memory"></a> [memory](#input\_memory) | The amount of memory to reserve for the Directus service | `number` | `4096` | no |
| <a name="input_rds_database_engine"></a> [rds\_database\_engine](#input\_rds\_database\_engine) | The engine of the RDS database | `string` | n/a | yes |
| <a name="input_rds_database_host"></a> [rds\_database\_host](#input\_rds\_database\_host) | The host of the RDS database | `string` | n/a | yes |
| <a name="input_rds_database_name"></a> [rds\_database\_name](#input\_rds\_database\_name) | The Name of the RDS database | `string` | n/a | yes |
| <a name="input_rds_database_password_secrets_manager_arn"></a> [rds\_database\_password\_secrets\_manager\_arn](#input\_rds\_database\_password\_secrets\_manager\_arn) | The ARN of the Secrets Manager secret containing the RDS database password | `string` | n/a | yes |
| <a name="input_rds_database_port"></a> [rds\_database\_port](#input\_rds\_database\_port) | The port of the RDS database | `number` | n/a | yes |
| <a name="input_rds_database_username"></a> [rds\_database\_username](#input\_rds\_database\_username) | The username of the RDS database user | `string` | n/a | yes |
| <a name="input_s3_bucket_name"></a> [s3\_bucket\_name](#input\_s3\_bucket\_name) | The name of the S3 bucket | `string` | `""` | no |
| <a name="input_subnet_ids"></a> [subnet\_ids](#input\_subnet\_ids) | The IDs of the subnets | `list(string)` | n/a | yes |
| <a name="input_tags"></a> [tags](#input\_tags) | The tags to apply to the resources | `map(string)` | `{}` | no |
| <a name="input_vpc_id"></a> [vpc\_id](#input\_vpc\_id) | The ID of the VPC | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_load_balancer_dns_name"></a> [load\_balancer\_dns\_name](#output\_load\_balancer\_dns\_name) | n/a |
| <a name="output_s3_bucket_arn"></a> [s3\_bucket\_arn](#output\_s3\_bucket\_arn) | n/a |
| <a name="output_s3_bucket_name"></a> [s3\_bucket\_name](#output\_s3\_bucket\_name) | n/a |


## Contributing

Contributions to this module are welcome! If you encounter any issues or have suggestions for improvements, please open an issue or submit a pull request on the GitHub repository.

## License

This module is open source and available under the [MIT License](https://opensource.org/licenses/MIT).
