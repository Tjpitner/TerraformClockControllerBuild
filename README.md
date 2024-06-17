This repo contains my build process for clock controller VM's using Terraform as well as the communication process between Oracle DB and our front end instance manager.

# Tech Stack:
Terraform

OCI

Bitbucket

Atlantis

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

Santity check: This guide assumes pwd returns your home directory or ~

Update your local copy & create a new git branch

```
cd ~/xxxx-oci_prd

git checkout master

git pull

git checkout -b clock-DATACENTER-CUSTOMER

mkdir DATACENTER/clock-controllers/CUSTOMER
```

# Create the flex shapes for OCI

```
/opt/xxxxxx/bin/newclock-flex.sh -e prd -d DATACENTER -c CUSTOMER -s 0 -p 2 -m 4 -M '100'
/opt/xxxxxx/bin/newclock-flex.sh -e tst -d DATACENTER -c CUSTOMER -s 0 -p 2 -m 4 -M '100'
```
# Validate the files for your Pull Request

```
cd DATACENTER/clock-controllers/CUSTOMER
git add -A .
git status
```

# Submit your Pull Request

```
git commit -m clock-DATACENTER-CUSTOMER
git push -u origin clock-DATACENTER-CUSTOMER
```

# Deploy Terraform Code
Make sure to merge the bitbucket request first and close the source branch

```
cd ~/xxxx-oci_prd
git checkout master
git pull
cd DATACENTER/clock-controllers/CUSTOMER
scl enable rh-python36 bash
tfv=1.1.7 . /xxxociprep
tfinit
terraform plan
terraform apply
```

# Deploy hosts with Rundeck

```
/opt/xxxxxx/bin/clock-rundeck-flex.sh
```

# Create DB User

Adding the prod/test clock controller user accounts to the instance frontend so the environments can communicate with the VM's

# Create password and create details in Crypto

Adding the clock controller DB user information and the newly created URL's to Crypto 









