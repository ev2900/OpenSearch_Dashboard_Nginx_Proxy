# OpenSearch Dashboard Nginx Proxy

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