### Purpose of these templates
The single template in this folder deploys an S3 bucket in the Log Archive account with a bucket policy that allows it to be used for recording flow logs for any compatible network resource in the organization.

The bucket policy follows best practices provided in the AWS documentation for [S3 bucket permissions for flow logs](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs-s3.html#flow-logs-s3-iam).

Bucket path prefixes are not supported: VPC flow logs must log to the root path of the S3 bucket. Hive-compatible S3 prefixes are supported.

Example usage:

``` yaml
MyVPC:
  Type: AWS::EC2::VPC
  Properties:
    CidrBlock: '10.100.0.0/16'

MyFlowLog:
  Type: AWS::EC2::FlowLog
  Properties:
    ResourceId: !Ref MyVPC
    ResourceType: VPC
    LogDestinationType: s3
    LogDestination: !Sub 'arn:aws:s3:::'${resourcePrefix}-flowlogs-${logArchiveAccountId}/'
    TrafficType: ALL
```
