```hcl
terraform {
  required_providers {
    proxmox = {
      source = "Telmate/proxmox"
      version = "3.0.1-rc2"
    }
  }
}

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

provider "proxmox" {
  pm_api_url = var.proxmox_api_url
  pm_api_token_id = var.proxmox_api_token_id
  pm_api_token_secret = var.proxmox_api_token_secret

 # When using SSCertificates and the client doesn't trust Proxmox UI
 # pm_tls_insecure = true
}
```

run `terraforn init` from this directory