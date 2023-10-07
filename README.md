# Recon-automata

This an Ansible playbook for deploying various recon tools on a remote server(-s). After configuring your inventory, you can easily install required tools on your server(-s) in one go.

Currently implemented tools are:

- [nmap](https://nmap.org/)
- [masscan](https://github.com/robertdavidgraham/masscan)
- [gau](https://github.com/lc/gau)
- [dnsvalidator](https://github.com/vortexau/dnsvalidator)
- [massdns](https://github.com/blechschmidt/massdns) - also a dependency of `puredns`
- [puredns](https://github.com/d3mondev/puredns)


> Note: this playbook was tested on Ubuntu Server 23.04 and may behave differently on other distros, e.g. those that use old versions of `golang` in repos. Work in progress!

## Usage

### Getting Ansible

First of all, you need to install Ansible. Manual can be found [here](https://docs.ansible.com/ansible/latest/installation_guide/index.html).

### Creating an inventory
Once you have installed Ansible, you need to create your inventory file. You can name it as you wish, but the general rule of thumb is to name it `hosts`. An example is provided in `hosts.example`:

```yaml
# ./hosts
all: # you can leave it as it is or create your own group
  hosts:
    my_host: # you can copy this block if multiple hosts are required
      ansible_host: 127.0.0.1 # remote machine address/domain name
      ansible_user: root # remote user
      ansible_password: yourpass # remote user's password
      ansible_become_password: yourpass # remote user's password again (for privileged operations)
```

### Group variables - tool selection
To specify the tools to install, change required parameters to `true` in [group vars file](./group_vars/all.yml).

If you created your own group in the inventory, create a file `./group_vars/YOUR_GROUP_NAME.yml` and specify the tools you need to install by setting variables like `install_%tool_name%: true`

For example, to install only `nmap` and `masscan` you can do this:

```yaml
# ./group_vars/your_group.yml
install_nmap: true
install_masscan: true
# All other tools will be defaulted to `false`.
```

### How to run

> Important: if you created your own group in the inventory, don't forget to change the name of the group in the playbook.

To run the playbook, use the following command:

```bash
$ ansible-playbook -i YOUR_INVENTORY_FILE setup.yml
```

If you wish to install all available tools, run another playbook available in the repo:

```bash
$ ansible-playbook -i YOUR_INVENTORY_FILE setup-all.yml
```