## Proxmox provider
`terraform.tf`
```
terraform {
  required_version = ">= 1.5"
  required_providers {
    proxmox = {
      source = "Telmate/proxmox"
      version = "3.0.1-rc2"
    }
  }
}
```

`variables.tf`
```
variable "proxmox_api_url" {
	type = string
}

variable "proxmox_api_token_id" {
	type = string
	sensitive = true
}

variable "proxmox_api_token_secret" {
	type = string
	sensitive = true
}

```

`_credentials.auto.tfvars`
```
# This file should be kept secret. Do not add to any repository

proxmox_api_url = "pve-api-url-here"

proxmox_api_token_id = "token-id-here"

proxmox_api_token_secret = "token-secret-here"

```

`main.tf`
```
provider "proxmox" {
  pm_api_url = var.proxmox_api_url
  pm_api_token_id = var.proxmox_api_token_id
  pm_api_token_secret = var.proxmox_api_token_secret

 # When using SSCertificates and the client doesn't trust Proxmox UI
 # pm_tls_insecure = true
}
```

run `terraforn init` from this directory