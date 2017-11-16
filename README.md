# AWS Sync

A Concourse pipeline for periodically syncing files from an S3 bucket in one AWS account to one in another.

## Configuration

Create a `secrets.yml` file:

```yaml
source_bucket: <name of source bucket>
region_source: <region of source bucket>
s3_access_key_source: <source account key>
s3_secret_key_source: <source account secret key>
destination_bucket: <name of destination bucket>
region_destination: <region of destination bucket>
s3_access_key_destination: <destination account key>
s3_secret_key_destination: <destination account secret key>
# example matcher: *.txt
# this will sync only txt files
matcher: <what files to sync>
# interval should match the format of the time resource
# https://github.com/concourse/time-resource#source-configuration
# i.e. 30m for 30 minutes
interval: <interval>
```

Set pipeline with:

```sh
fly -t target \
  set-pipeline -p sync \
  -c pipeline.yml \
  -l secrets.yml
```

Unpause and trigger manually.
