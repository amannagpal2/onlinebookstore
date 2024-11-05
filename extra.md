### **Variables used in aws-mq-broker**

| **Variable**                        | **Type**    | **Description**                                                                                 |
|-------------------------------------|-------------|-------------------------------------------------------------------------------------------------|
|`create_mq`| `bool`| Name of the s3 bucket storing code to be deployed in lambda functions|
|`mq_apply_immediately`| `bool` |	Specifies whether any cluster modifications are applied immediately, or during the next maintenance window|
|`mq_auto_minor_version_upgrade`| `bool` |Enables automatic upgrades to new minor versions for brokers, as Apache releases the versions |
|`mq_deployment_mode`|`string`| The deployment mode of the broker. Supported: SINGLE\_INSTANCE and ACTIVE\_STANDBY\_MULTI\_AZ |
|`mq_engine_type`|`string`| link to your eks cluster    |
|`mq_engine_version`|`string`| specifically required for ts_stimuli lambda function and contains the name/path of the ssm parameter that is storing the efs_id for this function    |
|`mq_host_instance_type`|`string`| can be enabled to deploy Tracker system for EC2 uptime     |
|`mq_publicly_accessible`|`bool`| specifically required for ts_stimuli lambda, is the name of the layer that stores the additional libraries needed for this function   |
|`mq_general_log_enabled`| `bool`| Name of the s3 bucket storing code to be deployed in lambda functions|
|`mq_audit_log_enabled`| `bool`| Name of the s3 bucket storing code to be deployed in lambda functions|
|`mq_admin_user`| `list(string)`| Name of the s3 bucket storing code to be deployed in lambda functions|
|`mq_application_user`| `list(string)`| Name of the s3 bucket storing code to be deployed in lambda functions|
|`cluster_security_group_id`| `string`| Name of the s3 bucket storing code to be deployed in lambda functions|
|`subnet_ids`| `list(string)`| Name of the s3 bucket storing code to be deployed in lambda functions|
|`vpc_id`| `string`| Name of the s3 bucket storing code to be deployed in lambda functions|
|`secret_name_format`| `string`| Name of the s3 bucket storing code to be deployed in lambda functions|
|`namespace`| `string`| Name of the s3 bucket storing code to be deployed in lambda functions|

