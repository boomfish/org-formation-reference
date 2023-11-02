### Purpose of these templates

The templates in this folder sets up an [AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html) [aggregator](https://docs.aws.amazon.com/config/latest/developerguide/aggregate-data.html) to collect configuration and compliance data into a delegated administrator account for the organization.

The update-stacks task binds the aggregator template to the security account. The bound account must be set up as a AWS Config delegated administrator for the organization prior to running these templates.

#### To enable AWS Config access to AWS Organizations

Run the following command from your organization management account:

```
aws organizations enable-aws-service-access --service-principal=config.amazonaws.com
```

Use the following command to verify the enable-aws-service-access command is complete:

```
aws organizations list-aws-service-access-for-organization
```

Under EnabledServicePrincipals, you should see config.amazonaws.com.

#### To register a delegated administrator account for AWS Config

To set up an aggregator from a non-management account, you must register a delegated admin account, which is a member account of your organization. From the management account, use the RegisterDelegatedAdministrator action to register a delegated admin. In the following AWS CLI command, replace MemberAccountID with the appropriate delegated admin account ID.

```
aws organizations register-delegated-administrator --service-principal config.amazonaws.com --account-id MemberAccountID
```

Note: The maximum number of delegated admins that the management account can assign for AWS Config (config.amazonaws.com) is 3.

Run the following command to verify the delegated admin has been registered successfully from the management account:

```
aws organizations list-delegated-administrators --service-principal=config.amazonaws.com
```
