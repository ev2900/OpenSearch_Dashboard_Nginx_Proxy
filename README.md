# OpenSearch Dashboard Nginx Proxy

Amazon OpenSearch services can deploy a domain in a private VPC, subnet(s). Deploying OpenSearch in a private subnet blocks traffic to the OpenSearch dashboard via. the public internet.

A Nginx proxy can be configured on an Ec2 in a public subnet (in the same VPC as the private subnet) to proxy traffic to the OpenSearch dashboard. **Enabling you to have a OpenSearch domain deployed in a private subnet with a OpenSearch dashboard accessable from the public internet**

Follow the instructions below

1. Run the CloudFormation stack below

[![Launch CloudFormation Stack](https://sharkech-public.s3.amazonaws.com/misc-public/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=os-nginx&templateURL=https://sharkech-public.s3.amazonaws.com/misc-public/opensearch_nginx.yaml)

The resources created by the CloudFormation stack are documented in the architecture below


<img alt="opensearch_nginx_yaml" src="https://github.com/ev2900/OpenSearch_Dashboard_Nginx_Proxy/blob/main/Read_Me_Architecture/ReadMe_Architecture.png">

# Install NGINX

sudo apt update
sudo apt install nginx

## SSL 

cd /etc/nginx/

# Private key

sudo openssl genrsa -des3 -out /etc/nginx/private.key 2048

# Public key

sudo openssl rsa -in private.key -out public.key

# CSR

sudo openssl req -new -key public.key -out certificate_signing_request.csr

# CRT

sudo openssl x509 -req -days 365 -in certificate_signing_request.csr -signkey public.key -out self_signed_certificate.crt

# NGIX 

cd sites-enabled

sudo vim default

*Replace the content of the default file*

sudo service nginx restart

# If needed ... 

sudo service nginx start
sudo service nginx stop

# Dashboard

*In your web-browser go to https://<ec2's-public-ip>/_dashboards*
