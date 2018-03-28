# MySQL installation pipeline

This pipeline and tasks installs and configures the MySQL v1 tile.

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

# mysql specific params (not actually optional)
optional_protections_recipient_email: nowhere@example.com
```
