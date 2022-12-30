## Initial Setup
- create & start AWS EC2 instance
- download SSH .cer file
- SSH into AWS EC2 instance

## Kafka Setup
- see kafka-setup.md

## Local Python Setup
- see py-setup.sh

## Setting up 'Streaming'
- create an AWS S3 bucket
- get AWS IAM user_credentials.csv / `brew install awscli` / `aws configure`
- use kafka-producer.ipynb to stream random data to Kafka
- use kafka-consumer.ipynb to consume data from Kafka (and write to S3)

## Query on AWS Athena
- setup AWS Glue Crawler on our S3 bucket
- query Glue Crawled data on AWS Athena

## [Useful Shell Commands Used](explainshell.com/explain)
- `ls -la` # aka <list all file/directories & permissions>
- `chmod 400 name-of-file.cer` # aka <set (read) file permission for EC2 secret.cer file>
- `ssh -i "name-of-file.cer" ec2-user@{IP}.eu-west-2.compute.amazonaws.com` # aka <connect to remote machine with local .cer secret>
- `lsof -i :2181` # aka <list open file, with internet address matching 2181 (Kafka Zookeeper)>
- `sudo kill -9 27439` # aka <kill running process with PID 27439>
