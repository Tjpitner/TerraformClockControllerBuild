This repo contains my build process for clock controller VM's using Terraform as well as the communication process between Oracle DB and our front end instance manager.

# Stack used:
Terraform

Bitbucket

Rundeck

Spacewalk

Nginx Load Balancer(s)

Check-MK

Crypto

# Validation

1. Validate customer requirements. Number of clocks?

2. Create Terraform Bitbucket Request

3. Deploy Terraform code

4. Deploy hosts with Rundeck

5. Add to Spacewalk

6. Configure load balancer

7. Create clock controller DB user

8. Create check_mk monitoring

9. Configure password and create Crypto entries

# Create Terraform Bitbucket Request
```
Santity check: This guide assumes pwd returns your home directory or ~

Update your local copy & create a new git branch

cd ~/wfstf-oci_prd

git checkout master

git pull

git checkout -b clock-DATACENTER-CUSTOMER

mkdir DATACENTER/clock-controllers/CUSTOMER
```






