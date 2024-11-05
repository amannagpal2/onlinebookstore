# Terraform-aws-pftp-global-resources
# Lambda
To begin with the creation of lambda resources you need to keep in mind the following main variables:

### **Key Variables**

| **Variable**                        | **Type**    | **Description**                                                                                 |
|-------------------------------------|-------------|-------------------------------------------------------------------------------------------------|
| `lambda_create`             | `bool`      | Controls the creation of the all Lambda resources. Set to ***`true`*** to create, or ***`false`*** to skip.       |
| `lambda_configs`                     | `map` | Contains all the variables required for lambda creation. |
| `lambda_functions` | `map` | Contains the definition of the lambda functions based on your requirements |

- Lambda Configuration requires a few values which would be used during specific lambda creations:

### **Variables inside lambda_configs**

| **Variable**                        | **Type**    | **Description**                                                                                 |
|-------------------------------------|-------------|-------------------------------------------------------------------------------------------------|
|`s3_bucket`| `string`| Name of the s3 bucket storing code to be deployed in lambda functions|
|`create_storage_bucket_kms_key`| `bool` | Controls the creation of KMS Key associated with the above s3 bucket. Required for certain lambdas. Set to ***`true`*** to create the key and ***`false`*** to not create the key|
|`costprotection_trigger`| `string` | time interval after which the costprotection function will be triggered `(eg. rate(15 minutes))`      |
|`costnotifier_trigger`|`string`| time interval after which the costnotifier function will be triggered `(eg. rate(15 minutes))` |
|`eks_oidc_url`|`string`| link to your eks cluster    |
|`efs_id_param_name`|`string`| specifically required for ts_stimuli lambda function and contains the name/path of the ssm parameter that is storing the efs_id for this function    |
|`enable_node_uptime_tracker`|`bool`| can be enabled to deploy Tracker system for EC2 uptime     |
|`ts_stimuli_layer_name`|`string`| specifically required for ts_stimuli lambda, is the name of the layer that stores the additional libraries needed for this function   |


- Inside the lambda_function map each function configuration should have a **create** variable. This create will be used in conjunction with lambda_create to be able to create a lambda. In case any of the following triggers need to be added ,kindly add the following parameters and set them as ***`true`***.
    ```   
    lambda_functions = {
      create_apigateway_trigger                  
      create_cloudwatch_notifier_trigger     
      create_cloudwatch_trigger              
      create_s3teamstorage_trigger
    } 
     ```
- Following is a sample of an expected configuration for lambda_function inside the **lambda_function** map
     ```  
     lambda_functions = {
      lambda_ts_stimuli = {    
          create                       = true    
          suffix                       = "ts_stimuli-lambda"    
          handler                      = "app.lambda_handler"    
          runtime                      = "python3.8"    
          timeout                      = 600    
          memory_size                  = 3008    
          description                  = ""    
          create_package               = false    
          local_existing_package       = "../../templates/
          python_existing_package.zip"    
          file_system_local_mount_path = "/mnt/efs"    
          create_apigateway_trigger    = false    
          attach_policy                = true    
          create_s3teamstorage_trigger = true    
          policy_statements = {     
              S3WriteTeamStorage = {        
                  effect    = "Allow"        
                  actions   = ["<Allowed Actions>"]        
                  resources = ["<ARN of the resources being used>"]      
                  },      
                  KMSWriteEncryptKeyTeamStorage = {        
                      effect  = "Allow"        
                      actions = ["<Allowed Actions>"]      
                      },    
                      }    
                      efs_file_id = "fs-057efc48e249f73d3"    
                      environment_variables = {      
                          LAMBDA_RUNTIME        = "CLOUD",      
                          STIMULI_FILE_MAX_SIZE = 2147483648,      
                          STIMULI_FILE_TEMP_DIR = "/mnt/efs",      
                          AWS_CONFIG_REGION     = "eu-central-1"    
                          }  
                          }
                        }
    ```
 



# License Server Setup

This repository provides infrastructure to set up and manage a License Server for various license management services, including **FlexNet**, **RLM**, and **FlexLM**, using Terraform. The configuration supports additional services such as **Promtail**, **Node Exporter**

## Key Variables
| **Variable**                        | **Type**    | **Description**                                                                                 |
|-------------------------------------|-------------|-------------------------------------------------------------------------------------------------|
| `license_server_create`             | `bool`      | Controls the creation of the License Server. Set to `true` to create, or `false` to skip.       |
| `license_server_configs`            | `map`       | Includes all information regarding the license instance, security, and S3 configurations.        |
| `root_zone_name`                    | `string`    | The root DNS zone name for the License Server.                                                  |
| `root_zone_id`                      | `string`    | The ID of the hosted DNS zone.                                                                  |
| `domain_name`                       | `string`    | The full domain name for the License Server.                                                    |
| `s3_bucket_id`                      | `string`    | The S3 bucket name where license-related files are stored.                                      |
| `nlb_create`                        | `bool`      | Controls NLB creation. Set to `true` to create, or `false` to skip.                             |
| `nlb_enable_deletion_protection`    | `bool`      | Controls deletion protection for NLB. Set to `true` to enable deletion protection.              |


## How to Add a New License File

To add a new license, follow these steps:

1. **Upload the License File**: Place the license file in the corresponding S3 folder (e.g., `flexnet`, `rlm`, `vlab`).
  
2. **Update the Configuration**: Modify the `.tfvars` file with the path to the new license in the appropriate section.

3. **Deploy the License Server**: Apply the changes and ensure the new license file is included.

4. **Verify the Updated License File**: Check that the new license has been recognized by the License Server.

## Testing License Server Availability

To ensure the License Server is running correctly, follow these steps:

1. **Access the EC2 Instance**:
   - Go to the AWS Management Console and locate the License Server EC2 instance.

2. **Connect to the Instance**: Use SSH to connect to the EC2 instance.

3. **Run Service Status Commands**: Execute the following commands to check the status of the various services:
### Service Status

- Check RLM service status: `service tracet-rlm status`
- Check Remote License Manager: `/opt/rlm/rlmutil rlmstat -a -c localhost@5085`
- Check FlexNet service status: `systemctl status flexnet.service`
- Check FlexNet license status: `/opt/flexnet/bin/lmutil lmstat -a -c /opt/flexnet/license/all.lic`


# API-Gateway creation 
- Below is the configurations followed for the creation of APIs.

## API Gateway Variables

| **Variable**         | **Type**   |**Description**                                                       |
|----------------------|------------|-----------------------------------------------------------------------|
| `api_gateway_create` | `bool`     | Controls the creation of any API Gateway.                             |
| `root_zone_name`     | `string`   | The root DNS zone name for the server.                                |
| `root_zone_id`       | `string`   | The ID associated with the root zone name.                            |
| `waf_name`           | `string`   | The WAF name associated with the AWS account.                         |
| `domain_configs`     | `map`      | Sub-domain name prefixes for Route 53 for A-record creation.           |
| `ipranges_edc_testing`| `list`    | List of IP ranges required for API creation.                          |
| `api_gateway_configs`   | `object`   | Configuration object for API Gateway setup, including NLB, certificates, and more. |
| `api_gateways`          | `map`      | Map of API Gateway configurations including both private and public types. |
| `name`               | `string`   | Name of the API Gateway.                                              |
| `path`               | `string`   | API Gateway path configuration.                                       |
| `endpoint_type`      | `string`   | Endpoint type for the API Gateway (`PRIVATE`, `REGIONAL`).             |
| `stage_name`         | `string`   | Stage name for the API Gateway.                                       |
| `template_path`      | `string`   | Path to the template file used for API Gateway creation.              |
| `lambda_arn_name`    | `string`   | ARN of the Lambda function associated with the API Gateway.           |
| `enable_policy`      | `bool`     | Controls whether a policy is enabled for the API.                     |


- Next is the main api-gateway creation where we pass the configurations that are required for the api. The modules divided into 2 types: **Private** and **Public**. Policies are attached based on whether the api is private or public.
- Following is the example of an expected private api-gateway configuration:
```
apigateway_costprotection_private = {
    create          = true
    name            = "costprotection-private"
    path            = "costprotection/costprotection"
    endpoint_type   = "PRIVATE"
    stage_name      = "pftp-tce-team"
    template_path   = "../../api/lambda_proxy_private_oauth_public_token.tpl"
    lambda_arn_name = "lambda_costprotection"
    enable_policy   = false
  }
```
- Following is the example of an expected public api-gateway configuration:
```
apigateway_campaign_service_keycloak = {
    create        = true
    name          = "campaign-service-keycloak"
    domain        = "consolev2.sre-euc1-sb.dev2.managed-runtime.bosch-mobility-cloud.com"
    path          = "campaign-service"
    endpoint_type = "REGIONAL"
    stage_name    = "sre-euc1-sb"
    template_path = "../../api/ms-camapign-service/4.1.0/public-keycloak.tpl"
  }
```
