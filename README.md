# Amazon ES Recommended Alarms - Automatically create and configure recommended CloudWatch alarms for Amazon Elasticsearch Service

## Introduction

The AmazonESRecommendedAlarm utility enables you to quickly create and manage CloudWatch metric alarms for your Amazon ES domain. Amazon ES domains send performance metrics to Amazon CloudWatch every minute. You can view the metrics and monitor the performance of your cluster in the Amazon Elasticsearch Service console. 

Hosting production grade Amazon ES cluster necessitates setting up alerts for critical metrics to send notification to operations team in case of any threshold breach. With Amazon CloudWatch, you can monitor your application workloads, create alarms, set thresholds for alarms.

CloudWatch alarm uses Simple Notification Service (SNS) to send notification in near-real time of any metric exceeds a specified value for some amount of time. For example, you might want AWS to email you if your cluster health status is red for longer than one minute.  Amazon ES recommends critical metrics you must setup alarm to avoid interruption for production cluster. Following are recommended alarm for Amazon ES cluster. For more information, see [Recommended CloudWatch Alarms](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/cloudwatch-alarms.html).

|Metric| Alarm|
| :--- | :--- |
| ClusterStatus.red | maximum is >= 1 for 1 minute, 1 consecutive time |
| ClusterStatus.yellow | maximum is >= 1 for 1 minute, 1 consecutive time |
| FreeStorageSpace | minimum is <= 20480 for 1 minute, 1 consecutive time |
| ClusterIndexWritesBlocked | is >= 1 for 5 minutes, 1 consecutive time |
| Nodes | minimum is < x for 1 day, 1 consecutive time |
| AutomatedSnapshotFailure | maximum is >= 1 for 1 minute, 1 consecutive time |
| CPUUtilization | maximum is >= 80% for 15 minutes, 3 consecutive times |
| JVMMemoryPressure | maximum is >= 80% for 5 minutes, 3 consecutive times |
| MasterCPUUtilization | maximum is >= 50% for 15 minutes, 3 consecutive times |
| MasterJVMMemoryPressure | maximum is >= 80% for 15 minutes, 1 consecutive time |
| KMSKeyError | is >= 1 for 1 minute, 1 consecutive time |
| KMSKeyInaccessible | is >= 1 for 1 minute, 1 consecutive time |

Following CloudFormation template lets you setup recommended alarms for your Amazon ES domain.  

## Getting Started
Following screenshot illustrates the parameters required to deploy the template. 
|Parameter|	Description|
| :--- | :--- |
| Amazon ES domain name | 	Enter the domain name (do not enter the endpoint) | 
| Total number of nodes | 	Enter the total No. of nodes in the cluster including data nodes, master nodes and UltraWarm nodes | 
| Dedicated master nodes | 	If domain has dedicated master nodes then enter Y, else N | 
| Encryption at rest | 	If domain has encryption enabled with Customer Master Key then enter Y, else N  | 
| Topic Name |  	Enter the SNS topic name. CloudFormation will add the stack name as suffix of the topic | 
| SNS Email	 | Enter the email address you want to get notification | 


## Walkthrough
1. Sign in to the console and choose the Region of Amazon ES cluster

2. Launch the stack specific to your region

      | Region | CloudFormation |
      |--------|----------------|
      | N. Virginia (us-east-1) |[![Deploy in us-east-1](./images/cloudformation-launch-stack-button.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/review?stackName=Amazon-ES-Recommended-Alarms&templateURL=https://cf-templates-1djmokk063kxm-us-east-1.s3.amazonaws.com/elasticsearch-recommended-alarms.yaml) |
      | Oregon (us-west-2) |[![Deploy in us-west-2](./images/cloudformation-launch-stack-button.png)](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/create/review?stackName=Amazon-ES-Recommended-Alarms&templateURL=https://cf-templates-1djmokk063kxm-us-west-2.s3-us-west-2.amazonaws.com/elasticsearch-recommended-alarms.yaml) |
      | Frankfurt (eu-central-1) |[![Deploy in eu-central-1](./images/cloudformation-launch-stack-button.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-central-1#/stacks/create/review?stackName=Amazon-ES-Recommended-Alarms&templateURL=https://cf-templates-1djmokk063kxm-eu-central-1.s3.eu-central-1.amazonaws.com/elasticsearch-recommended-alarms.yaml) |
      | Ireland(eu-west-1) |[![Deploy in eu-west-1](./images/cloudformation-launch-stack-button.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/create/review?stackName=Amazon-ES-Recommended-Alarms&templateURL=https://cf-templates-1djmokk063kxm-eu-west-1.s3-eu-west-1.amazonaws.com/elasticsearch-recommended-alarms.yaml) |
      | Singapore(ap-southeast-1) |[![Deploy in ap-southeast-1](./images/cloudformation-launch-stack-button.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/create/review?stackName=Amazon-ES-Recommended-Alarms&templateURL=https://cf-templates-1djmokk063kxm-ap-southeast-1.s3-ap-southeast-1.amazonaws.com/elasticsearch-recommended-alarms.yaml) |

    If your region doesn't list above, use manually this template.

    ```text
    https://aes-siem-<REGION>.s3.amazonaws.com/siem-on-amazon-elasticsearch.template
    ```

3. Enter your Amazon ES cluster details as shown in the following screenshot. 
![Sample parameters](./images/cloudformation-parameters.png)

4. Choose Create stack.

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

