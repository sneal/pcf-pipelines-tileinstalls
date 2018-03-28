# RabbitMQ installation pipeline

This pipeline and tasks installs and configures the RabbitMQ tile.

## Usage

Create a Concourse parameter yaml file with the environment specific fields required by the pipeline. Here's a sample:

```
# legacy pivnet token for downloading tile
pivnet_token: nGc-x0heYcz-dsxtNCyw

# opsman connection info
opsman_domain_or_ip_address: opsman.aws-pcf.example.com
opsman_admin_username: admin
opsman_admin_password: secret

# required network config
singleton_jobs_az: us-west-2b
other_azs: us-west-2b,us-west-2c
network_name: services
services_network_name: dynamic-services

# rabbitmq specific params
on_demand_broker_plan_1_rabbitmq_az_placement: us-west-2b
server_admin_username: rabbitadmin
server_admin_password: secret
```
