# J LSF resource connnector


!!! abstract 
    概述
    

## LSF resource connector overview

## Configuring resource providers
- [ ] Setting the initial configuration
- [ ] Configuring multiple resource providers
- [ ] Configuring different templates to create instances
- [ ] Assigning exclusive resources to a template
- [ ] Configuring IBM Spectrum Conductor with Spark for LSF resource connector
    - [ ] Managing resource sharing and distribution
    - [ ] Installing LSF on compute hosts
    - [ ] Configure resource connector for IBM Spectrum Conductor with Spark
    - [ ] Submitting jobs to EGO
        - [ ] How LSF returns hosts to EGO
- [ ] Configuring IBM Bluemix for LSF resource connector
    - [ ] Configuring LSF resource connector for IBM Bluemix
    - [ ] Submitting jobs to IBM Bluemix
- [ ] Configuring OpenStack for LSF resource connector
    - [ ] Configuring the DNS server for OpenStack
    - [ ] Configuring resource connector for OpenStack
    - [ ] Submitting jobs to OpenStack
        - [ ] How LSF returns hosts to OpenStack
- [ ] Configuring Microsoft Azure for LSF resource connector
    - [ ] Configuring LSF resource connector for Microsoft Azure
    - [ ] Update the LSF configuration for Microsoft Azure
    - [ ] Submitting jobs to Microsoft Azure
    - [ ] Adding multiple Azure providers
- [ ] Configuring Microsoft Azure CycleCloud for LSF resource connector
    - [ ] Configuring LSF resource connector for Microsoft Azure CycleCloud
    - [ ] Update the LSF configuration for Microsoft Azure CycleCloud
    - [ ] Submitting jobs to Microsoft Azure CycleCloud
- [ ] Configuring Google Cloud Platform for LSF resource connector
    - [ ] Configuring LSF resource connector for Google Cloud Platform
    - [ ] Submitting jobs to Google Cloud Platform
- [ ] Configuring Amazon Web Services for LSF resource connector
    - [ ] Preparing to configure AWS
    - [ ] Building a cloud image
        - [ ] Preparing Amazon Web Services components
        - [ ] Launching the Amazon Web Services EC2 instance
        - [ ] Installing an LSF server host on the AWS EC2 instance
    - [ ] Enabling LSF resource connector for Amazon Web Services (AWS)
        - [ ] The aws_enable.sh script
        - [ ] Choose account authentication method
        - [ ] Executing AWS enablement script for LSF
        - [ ] Completing the enabling of Resource Connector for AWS
            - [ ] Configuring user scripts to register AWS hosts
    - [ ] Configuring Bursting Behavior
        - [ ] Configuring a threshold
        - [ ] Providing specific policy configurations
        - [ ] Controlling reclaim behavior
    - [ ] Assigning exclusive resources to a template
    - [ ] Configuring AWS access with federated accounts
    - [ ] Configure AWS launch templates
    - [ ] Attach EFA network interfaces
    - [ ] Use AWS spot instances
        - [ ] Configuring AWS Spot instances
    - [ ] Submitting jobs to AWS
        - [ ] How LSF returns hosts to AWS
- [ ] Configuring OpenShift for LSF resource connector
    - [ ] Enabling LSF resource connector for OpenShift
    - [ ] Submitting jobs to OpenShift
- [ ] Configuring IBM Cloud Gen 2 for LSF resource connector
    - [ ] Preparing IBM Cloud Gen 2 for LSF resource connector
    - [ ] Configuring LSF resource connector for IBM Cloud Gen 2
    - [ ] Submitting jobs to IBM Cloud Gen 2

## Updating LSF configuration for resource connector
- [ ] Pre-provisioning and post-provisioning
- [ ] Define resource provisioning policies
- [ ] Use the LSF patch installer to update resource connector

## View information on the LSF resource connector
- [ ] Checking the LSF resource connector status
- [ ] Use badmin to view LSF resource connector information
- [ ] Logging and troubleshooting

## Configuration reference
- [ ] lsb.applications
    - [ ] RC_ACCOUNT
    - [ ] RC_RECLAIM_ACTION
- [ ] lsb.queues
    - [ ] RC_ACCOUNT
    - [ ] RC_DEMAND_POLICY
    - [ ] RC_HOSTS
- [ ] lsf.conf
    - [ ] LSB_RC_DEFAULT_HOST_TYPE
    - [ ] LSB_RC_EXTERNAL_HOST_FLAG
    - [ ] LSB_RC_EXTERNAL_HOST_IDLE_TIME
    - [ ] LSB_RC_EXTERNAL_HOST_MAX_TTL
    - [ ] LSB_RC_MQTT_ERROR_LIMIT
    - [ ] LSF_MQ_BROKER_HOSTS
    - [ ] LSB_RC_QUERY_INTERVAL
    - [ ] LSB_RC_REQUEUE_BUFFER
    - [ ] LSB_RC_TEMPLATE_REQUEST_DELAY
    - [ ] LSB_RC_UPDATE_INTERVAL
    - [ ] MQTT_BROKER_HOST
    - [ ] MQTT_BROKER_PORT
    - [ ] EBROKERD_HOST_CLEAN_DELAY
- [ ] egoprov_config.json
- [ ] egoprov_ego.conf
- [ ] egoprov_templates.json
- [ ] hostProviders.json
- [ ] osprov_config.json
- [ ] osprov_templates.json
- [ ] policy_config.json
- [ ] awsprov_config.json
- [ ] awsprov_templates.json
- [ ] azureprov_config.json
- [ ] azureprov_templates.json
- [ ] cyclecloudprov_config.json
- [ ] cyclecloudprov_templates.json
- [ ] softlayerprov_config.json
- [ ] softlayer_templates.json
- [ ] googleprov_config.json
- [ ] googleprov_templates.json
- [ ] openshiftprov_config.json
- [ ] openshiftprov_templates.json
- [ ] ibmcloudgen2_config.json
- [ ] ibmcloudgen2_templates.json
