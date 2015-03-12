# my-account

- Create a first user after a base image install of a node
- Install user ssh pub keys from various sources:
  - List of default file locations
	- ~{{user}}/.ssh/id-rsa.pub
	- ~{{user}}/.ssh/id-dsa.pub
  - List of keys in ansible var
  - List of key files in ansible var
  - List of keys from a `github` acount

## Requirements

- Automatic install of `python-httplib2` package if user ssh pub keys fetched from `github`
- Tested with ansible 1.8. Probably works with earlier version but use
  `skipped` filter and registered loop

## Role Variables

``` yaml
my_account_user: guest              # user to create
my_account_name: Guest User         # GECOS field
my_account_shell: /bin/bash         # default shell
my_account_ssh_pub_keys: []         # list of keys
#  - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCvpcV/YrKWewCJmN7pwF1uJRKrQwuD2NrD/PA1OEa/Hh9ykbc/rC3dtXgCQ5QtDzQ2ZFwG4BIEZKywFv/AyogwI7L4K6n7MrI5G64lubmyHTnNzdcMIgrPwSloZbPCLx+Pb6FqR2oDhq7kow7yr1HPl2iCWM/iVQqKVcxyVUqnREQCMlhqxyJA6jTUAaknfZQYDB1qASjMQEkvrIPlzMHEAEGKlaAgUxUnwU8YITyge/QxuD7RGoqALgihm+We0BbQKTuRv8cRkgmICr/MDSnT+Lz4CXcB0iHPU6cyZ90sgoxER0YTWA9XhTpOBtHHRrV6sdWGDcYncVaoSob7jUUj
my_account_ssh_pub_key_files: []    # list of key files
#  - ~guest/.ssh/guest-id_rsa.pub
#  - ~guest/.ssh/guest-id_dsa.pub
my_account_github_user: guest       # github account
my_account_use:                     # a list of keys sources to use
  - keys                            # use the list of keys
  - key_files                       # use list of key files
  - std_files                       # use default key files
  - github                          # use github account
```

## Dependencies

None

## Example Playbook

```
- hosts: newhost
  gather_facts: no

  roles:
    - role: thydel.my-account
      my_account_user: thy
      my_account_name: Thierry Delamare
      my_account_github_user: thydel
      my_account_use:
        - std_files
		- github
```

## License

MIT

## Author Information

Thierry Delamare
