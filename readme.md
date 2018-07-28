# terraform-aws-sns-to-cloudwatch-logs-lambda

[![Latest Release](https://img.shields.io/github/release/robertpeteuil/terraform-aws-sns-to-cloudwatch-logs-lambda.svg)](https://github.com/robertpeteuil/terraform-aws-sns-to-cloudwatch-logs-lambda)[![license](https://img.shields.io/github/license/robertpeteuil/terraform-aws-sns-to-cloudwatch-logs-lambda.svg?colorB=2067b8)](https://github.com/robertpeteuil/terraform-aws-sns-to-cloudwatch-logs-lambda)

`terraform-aws-sns-to-cloudwatch-logs-lambda` is a Terraform module to provision a Lambda Function that routes SNS messages to CloudWatch Logs

## Terraform Module Features

Terraform Module allows simple and rapid deployment

- Creates Lambda function, IAM Policies, Triggers, and Subscriptions
- Creates (or use existing) SNS Topic, CloudWatch Log Group and Log Group Stream
- Options:
  - Create CloudWatch Event to prevent Function hibernation
  - Set Log Group retention period

## SNS to CloudWatch Logs Features

Lambda Function forwards subject & body of SNS messages to CloudWatch Log Group Stream

- Enhance the value of CloudWatch Logs by allowing entry creation from virtually any service, notification or script
- Enable cloud-init, bootstraps and functions to easily write entries to CloudWatch Logs
- Easily add instrumentation to shell-scripts: `aws sns publish --topic-arn $TOPIC_ARN --message $LOG_ENTRY`
- Troubleshoot script, function and service spread across resources

## Usage

``` ruby
module "sns_gw" {
  source            = "git::https://github.com/robertpeteuil/terraform-aws-sns-to-cloudwatch-logs-lambda?ref=tags/0.1.0"
  aws_region        = "us-west-2"
  sns_topic_name    = "logging"
  log_group_name    = "project"
  log_stream_name   = "snslogs"
}
```

> NOTE: Make sure you are using [version pinning](https://www.terraform.io/docs/modules/usage.html#module-versions) to avoid unexpected changes when the module is updated.

## Required Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| aws_region | Region where AWS resources are located | string | - | yes |
| sns_topic_name | Name of SNS Topic to be logged by Gateway | string | - | yes |
| log_group_name | Name of CloudWatch Log Group | string | - | yes |
| log_stream_name | Name of CloudWatch Log Stream | string | - | yes |

## Optional Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| create_sns_topic | Create new SNS topic | string | `true` | no |
| create_log_group | Create new log group | string | `true` | no |
| create_log_stream | Create new log stream | string | `true` | no |
| log_group_retention_days | Log Group retention (days) | string | `0 (forever)` | no |
| lambda_func_name | Name for Lambda Function | string | `SNStoCloudWatchLogs` | no |
| lambda_description | Lambda Function Description | string | `Route SNS messages to CloudWatch Logs` | no |
| lambda_publish_func | Publish Lambda Function | string | `false` | no |
| create_warmer_event | Create CloudWatch trigger event to prevent hibernation | string | `false` | no |
| lambda_timeout | Function time-out (seconds) | string | `3` | no |
| lambda_mem_size | Function RAM assigned (MB) | string | `128` | no |
