# tf-aws-pi-hole
## Complete Terraform solution to Pi Hole install

Many thanks to the guys and gals that actually provide this free opensource tool for the benefit of us all.
https://pi-hole.net/


## Overview

This repo is responsible for managing/creating an ec2 instance inside of aws free tier t2.micro with an elastic ip address and deploying pihole preconfigured into that instance

Also configured if you use version 2.#.# onwards is the ability to have a pre-configured openvpn instance too so not jsut the dns is filtered but all traffic can then go down the vpn too

## Prerequisites

* A basic knowledge of terraform , how to apply and run it.
* A basic understanding of how to configure / setup and use aws cli commands. -- You will need to setup appropriate profile

##NB
* It is recommended that you setup/and use a remote state.


## Versions

See change log for specifics.

1.#.# >= only the Pi Hole deployment (Now this works we are probably not expecting much more to be added here except standard updates/patches)
2.#.# >= both the Pi Hole and OpenVPN

## Usage

Setup which state storage you want to use. By default it will assume backend remote state storage.
If you do want to use with remote state make sure you run `terraform apply` in the `backend-state` folder to release the needed infra for remote state storage
If you dont want to use remote state remove the following from the versions.tf file 
```
  backend "s3" {
    key = "terraform-aws/pihole_openvpn/terraform.tfstate"
  }
```

Then simply run `terraform apply` in the parent terraform directory and provide the variables required. It will create the rest.

Or include the variables in a parameter file like `terraform apply -var-file=params/default.tfvars`

## Future features

* SG to ensure there is always a running instance
* ariablised instance type so that it can be run on other instance types instead of just t2.mico (free tier)
* Variablised hostname to pass into the pihole ec2 setup
* Completed permissions map for the bespoke created IAM user/role/policy

# !!!! DISCLAIMER !!!!

All code is currently designed to run within aws free tier. However there are still certain costs associated with running infra in aws. All costs are down to the responsibility of the aws account owner. If you dont know/understand what this is deploying. Dont deploy it. There may be running costs involved with elastic ips/storage/keypairs that you as the aws account owner would be responsible for.
