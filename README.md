## What's this?
This is a stack used to host Grafana and InfluxDB behind nginx. Please note that this is running on a single EC2 instance, so it's intentionally not highly available.

## High level architecture overview
- EC2 instance for hosting Grafana, InfluxDB and nginx with encrypted EBS volumes (root, swap, data)
- Elastic IP for the instance
- All resources isolated in a VPC

## Requirements
- Latest version of Packer
- Latest version of Ansible

## Building the base image
```
ansible-galaxy install -p playbook/galaxy -r playbook/requirements.yml
packer build base-image.json
```
The resulting AMI ID should be supplied to CloudFormation when building the stack in the `InstanceAMI` parameter.

## First time configuration
After setting up the stack for the first time, it requires some manual configuration. You have to configure nginx to forward requests to Grafana and InfluxDB, and you have to set up TLS on your own domain yourself.
