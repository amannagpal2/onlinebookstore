### **Variables inside lambda_configs**

| **Variable**                        | **Type**    | **Description**                                                                                 |
|-------------------------------------|-------------|-------------------------------------------------------------------------------------------------|
|`create_mq`| `string`| Name of the s3 bucket storing code to be deployed in lambda functions|
|`mq_apply_immediately`| `bool` | Controls the creation of KMS Key associated with the above s3 bucket. Required for certain lambdas. Set to ***`true`*** to create the key and ***`false`*** to not create the key|
|`mq_auto_minor_version_upgrade`| `string` | time interval after which the costprotection function will be triggered `(eg. rate(15 minutes))`      |
|`mq_deployment_mode`|`string`| time interval after which the costnotifier function will be triggered `(eg. rate(15 minutes))` |
|`mq_engine_type`|`string`| link to your eks cluster    |
|`mq_engine_version`|`string`| specifically required for ts_stimuli lambda function and contains the name/path of the ssm parameter that is storing the efs_id for this function    |
|`mq_host_instance_type`|`bool`| can be enabled to deploy Tracker system for EC2 uptime     |
|`mq_publicly_accessible`|`string`| specifically required for ts_stimuli lambda, is the name of the layer that stores the additional libraries needed for this function   |
