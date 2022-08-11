# F5-XC-ORIGIN-POOL
This repository consists of Terraform templates to create a F5XC Origin Pool object.

## Usage

- Clone this repo with: `git clone --recurse-submodules https://github.com/cklewar/f5-xc-origin-pool`
- Enter repository directory with: `cd f5-xc-origin-pool`
- Obtain F5XC API certificate file from Console and save it to `cert` directory
- Pick and choose from below examples and add mandatory input data and copy data into file `main.tf.example`.
- Rename file __main.tf.example__ to __main.tf__ with: `rename main.tf.example main.tf`
- Initialize with: `terraform init`
- Apply with: `terraform apply -auto-approve` or destroy with: `terraform destroy -auto-approve`

## Origin pool module usage example

```hcl
variable "project_prefix" {
  type        = string
  description = "prefix string put in front of string"
  default     = "f5xc"
}

variable "project_suffix" {
  type        = string
  description = "prefix string put at the end of string"
  default     = "01"
}

variable "f5xc_api_p12_file" {
  type = string
}

variable "f5xc_api_url" {
  type = string
}

variable "f5xc_tenant" {
  type = string
}

module "origin_pool_private_ip_site" {
  source                                             = "./modules/f5xc/origin-pool"
  f5xc_tenant                                        = var.f5xc_tenant
  f5xc_api_url                                       = var.f5xc_api_url
  f5xc_api_p12_file                                  = var.f5xc_api_p12_file
  f5xc_namespace                                     = "system"
  f5xc_origin_pool_name                              = format("%s-pool-private-ip-site-%s", var.project_prefix, var.project_suffix)
  f5xc_origin_pool_port                              = "443"
  f5xc_origin_pool_private_ip                        = "10.15.250.100"
  f5xc_origin_pool_private_ip_site_locator_site_name = "refMySite"
  f5xc_origin_pool_private_ip_inside_network         = false
  f5xc_origin_pool_private_ip_outside_network        = true
  f5xc_origin_pool_labels                            = {
    Label1 = "value1"
  }
}
```
