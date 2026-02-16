# Terraform commands
#Terraform #IaC #Automation

## Edit the configuration files to hashicorp’s standards
```bash
terraform fmt
```

## Initialise terraform
Installs providers.
```bash
terraform init
```

## Checks for errors.
Confirms that the configuration is valid
```bash
terraform validate
```

## Generate an execution plan
```bash
terraform plan
```
Write a plan file to the given path. This can be used as input to the "apply" command.
```bash
terraform -out=plan/file/path
```

## Apply configuration
```bash
terraform apply
```

```bash
terraform apply plan/file/path
```

## List resources and data sources in your terraform workspace’s state
```bash
terraform list state
```

## List the entire workspace’s state
```bash
terraform show
```

## Overriding variable values. 
(Assuming the is a variable named “instance_type” defined)
```bash
terraform plan -var instance_type=t2.large
```


## Destroy all deployed assets
```bash
terraform destroy
```

## Destroy specific hosts
```bash
terraform plan -destroy \\
  -target='proxmox_vm_qemu.masters[0]' \\
  -target='proxmox_vm_qemu.masters[1]' 
```

```bash
terraform % terraform destroy \\
  -target='proxmox_vm_qemu.masters[0]' \\
  -target='proxmox_vm_qemu.masters[1]'
```

## Review output values
```bash
terraform output
```
