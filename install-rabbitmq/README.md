# RabbitMQ installation pipeline

This pipeline and tasks installs and configures the RabbitMQ tile.

## Usage

At the root of the repository create a Concourse parameter yaml file with the environment specific fields required by the tile's pipeline. In this example we'll assume you named your parameters file `sandbox-params.yml`. Here's a sample params file with the required fields filled out for this pipeline:

```
# legacy pivnet token for downloading tile
pivnet_token: ((pivnet_token))

# opsman connection info
opsman_domain_or_ip_address: opsman.sandbox.example.com
opsman_admin_username: admin
opsman_admin_password: ((sandbox_opsman_admin_password))

# required network config
singleton_jobs_az: us-west-2b
other_azs: us-west-2b,us-west-2c
network_name: services
services_network_name: dynamic-services

# rabbitmq specific params
on_demand_broker_plan_1_rabbitmq_az_placement: us-west-2b
server_admin_username: rabbitmqadmin
server_admin_password: ((sandbox_rabbitmq_admin_password))
```

It's _highly_ recommended to use CredHub to store sensitive values like passwords and keys. You should commit your environment specific parameters file to git for auditability, tile configuration changes, and complete environment rebuilds.

With the required pipeline parameters file created we need to generate the actual tile pipeline from the pipeline.yml at the root of the repo and the pipeline-patch.yml ops file. Once generated we can fly up the pipeline. In the below example we're targeting a Concourse instance/team named sandbox and creating a pipeline named `deploy-rabbitmq`.

```
$ cat pipeline.yml | yaml-patch -o install-rabbitmq/pipeline-patch.yml > rabbitmq-pipeline.yml
$ fly -t sandbox set-pipline -p deploy-rabbitmq -c rabbitmq-pipeline.yml -l install-rabbitmq/params.yml -l sandbox-params.yml
```

Once the pipeline is fly'd up to Concourse we can unpause the pipeline and kick off a run.
