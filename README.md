# pks-gcp-quickstart

testing

This repo contains a concourse pipeline and tasks to automatically deploy PKS on GCP, including paving the environment using Terraform. This is meant for POCs and getting a minimal platform up quickly in a self contained way. this should not be used for production.
It is using [terraforming-gcp](https://github.com/pivotal-cf/terraforming-gcp) and [Platform Automation](http://docs.pivotal.io/platform-automation/v2.2/) to do so.

# Features

* deploys PKS as well as an initial cluster
* the pipeline can be deployed multiple times with different values for `env_name`
  * for each pipeline there will be a dedicated subdomain created in gcp: `env_name.dns_suffix`
* letsencrypt certificates are generated for PKS and Ops Manager.\

# Reqirements

* GCP account
* Pivotal Network account
* Git Repository
* 1 private GCS Bucket
* concourse(local if neccessary)
* a (sub-)domain hosted on GCP

# Credentials

To keep it simple and easy deployable on any concourse installation, the pipeline currently gets most of its credentials and customization fron a `credentials.yml` file.
Copy the `credentials-template.yml` file to `credentials.yml` and modify the appropriate items.

# Deploy Pipline

```
docker-compose up
fly login -t local -c  http://localhost:8080
fly -t local set-pipeline -p pks-gcp-quickstart -c pipeline.yml -l credentials.yml --verbose
fly -t local unpause-pipeline -p pks-gcp-quickstart
```
