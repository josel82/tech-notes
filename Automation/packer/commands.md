
## Validate configuration files
```bash
packer validate -var-file='../credentials.pkr.hcl' ubuntu-server-focal.pkr.hcl
```
The `-var-file` flag provides a more secure way to get sensitive data into the configuration file. the file containing the sensitive information should be kept safe, and should not be added to the repository.

## Deploy
```bash
packer build -var-file='../credentials.pkr.hcl' ubuntu-server-focal.pkr.hcl
```
