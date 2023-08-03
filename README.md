# Recon-automata

This an Ansible playbook for deploying various recon tools on a remote server. After configuring your inventory, you can easily install required tools on your servers in one go.

Currently implemented tools are:

- [nmap](https://nmap.org/)
- [masscan](https://github.com/robertdavidgraham/masscan)
- [gau](https://github.com/lc/gau)
- [dnsvalidator](https://github.com/vortexau/dnsvalidator)
- [puredns](https://github.com/d3mondev/puredns)


> Note: this playbook was tested on Ubuntu Server 23.04 and will work only on Debian-based distros.

## Usage

First of all, you need to install Ansible. Manual can be found [here](https://docs.ansible.com/ansible/latest/installation_guide/index.html).

Once you have installed Ansible, you need to create your inventary. You can name it as you wish, but the general rule of thumb is to name it `hosts`. An example is provided in `hosts.example`:

```yaml
# ./hosts
all: # IMPORTANT: change 'all' to your own group name
  hosts:
    host1: # you can copy this block if multiple hosts are required
      ansible_host: 127.0.0.1 # remote machine address/domain name
      ansible_user: root # remote user
      ansible_password: yourpass # remote user's password
      ansible_become_password: yourpass # remote user's password again (for privileged operations)
```
If you need to install all the tools provided in the repo, you can name your group as `all_true`. There is an already prepared config file for this case.

If you need only specific tools, create a file `./group_vars/YOUR_GROUP_NAME.yml`. Specify the tools you need to install by setting variables like `install_%tool_name%: true`

For example, to install only `nmap` and `masscan` you can do this:

```yaml
# ./group_vars/your_group.yml
install_nmap: true
install_masscan: true
```

All other tools are defaulted to `false`. To run the playbook, use the following command:

```bash
$ ansible-playbook -i YOUR_INVENTORY_FILE setup.yml
```