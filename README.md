# ansible-hcloudservers
Ansible playbook and role to create hetzner cloud server

## Project dependencies

### Python
* [netaddr](https://pypi.org/project/netaddr/)
* [jmespath](https://pypi.org/project/jmespath/)
* [hcloud-python](https://pypi.org/project/hcloud/)

```bash
pip install netaddr
pip install jmespath
pip install hcloud
```

### Hetzner Account
* [Cloud Console](https://console.hetzner.cloud/projects)
* [DNS Console](https://dns.hetzner.com/)

## Vault files
### Vault file "group_vars/all/vault"
Create the vault file "group_vars/all/vault"
```bash
touch group_vars/all/vault
ansible-vault encrypt group_vars/all/vault
ansible-vault edit group_vars/all/vault
```
and paste the following content to the generated vault file:

```yaml
# groupvars/all/vault
vault_hetzner_dns_token: "<InsertHetznerDNSApiTokenHere>"
vault_hetzner_dns_token: "<InsertHetznerDNSZoneIdHere>"
vault_local_user_ssh_key_name_01: "<user@host1>"
vault_local_user_ssh_key_name_02: "<user@host2>"
```

### Vault file "group_vars/hcloudservers/vault"
Create the vault file "group_vars/hcloudservers/vault"
```bash
touch group_vars/hcloudservers/vault
ansible-vault encrypt group_vars/hcloudservers/vault
ansible-vault edit group_vars/hcloudservers/vault
```

```yaml
# group_vars/hcloudservers/vault
vault_hcloud_token: "<InsertHetznerApiTokenHere>"
```

## Ansible
### Play

Create all hcloudservers
```bash
ansible-playbook --ask-vault -i inventory site.yml
```

Delete all hcloudservers
```bash
ansible-playbook --ask-vault -i inventory site.yml --tags=hcloud_cleanup
```

### Available tags
* hcloud_info - Print Hetzner datacenter and location information
* hcloud_cleanup - Delete servers
