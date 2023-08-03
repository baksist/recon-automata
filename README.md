# Recon-automata

This an Ansible playbook for deploying various recon tools on a remote server. After configuring your inventory, you can easily install required tools on your servers in one go.

To install all the tools, run:

```bash
$ ansible-playbook -i hosts setup.yml
```

If you wish to install only specific tools, run:

```bash
$ ansible-playbook -i hosts setup.yml -t tool,another_tool
```

Currently implemnted tools are:

- [nmap](https://nmap.org/)
- [masscan](https://github.com/robertdavidgraham/masscan)
- [gau](https://github.com/lc/gau)
- [dnsvalidator](https://github.com/vortexau/dnsvalidator)
- [puredns](https://github.com/d3mondev/puredns)