# vaultfs
Hashicorp Vault fuse filesystem

The intent for this package is to get secrets from the vault server if the secret is not found in the local path.

## Setup

```bash
git clone 
cd vaultfs
sudo python3.6 setup.py install
```

## Usage

```bash
usage: vaultfs [-h] [-c] -m  -l  -r  -s  -p

Vault fuse file system

optional arguments:
  -h, --help            show this help message and exit
  -c , --config         Config file.
  -m , --mountpoint     where the fuse filesystem will be mounted.
  -l , --local          credentials local path after being pulled from vault.
  -r , --remote         Vault Server HTTPS address.
  -s , --secrets-path   List of secrets path in the Vault server.
  -p , --payload        Vault authentication token.
```

*This is a WIP*

*THis is what we want to implement*

- This module requires a mountpoint,a local path and the remote url of the hashicorp vault

- It will also requires a:
  * Token (`payload`) that will allow `vaultfs` to authenticate requests made to the vault 
  * List of secret engines from where secrets will be fetched ( this requires that the token has enought permissions to access those ).
  * data_key: Given that the vault will store secrets in KV2 (currently kv will not be supported) backend, we need to specify the key where the secrets are stored.
  

the system/human will expect files to be in the mountpoint, `vaultfs` will first fetch them from the vault and copy them to the local path, hitherto the system/programs/human can find the file in the expected destination.

TODO:
- Make sure the program checks vault for existing file for new version. (use hashlib)
- Hardin the logging
- Implement rotating token and generating them from a role id. (maybe ?)
- Implement getting configs from a file (that we may put in /etc/)
