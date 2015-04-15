# ansible-consul-demo
Demo of Consul and Ansible

## Installation

1. Spin-up some Ubuntu servers on AWS (or any other hosting)
1. Edit the IPs of the servrs in the provided `hosts` file (present at the 
same level as this README)
2. Make sure to also edit `group_vars/all.yml" and enter the IP(s) of all servers
   that you allocated as consul servers. The entries in hosts and group_vars.all.yml
   must correspond to each other!
1. In AWS EC2, the root username for Ubuntu servers is called: `ubuntu`. If you 
spin your servers up somewhere where that is not the case, edit 
`group_vars/all.yml` and modify the value of the `ansible_ssh_user: ubuntu` variable.
1. Create `ssh` folder under this checkout (same level as README)
1. Save a private SSH key that corresponds to the root user on all your new servers
   under: `ssh/private-key.pem`
1. Make sure your private key permissions are valid:
       
       ```consul
       chmod 700 ssh
       chmod 600 ssh/*
       ```
1. Make sure you have at least following ports open on public IPs
    ![](http://media.froyo.io/image/1U1h1w2a021h/EC2_Management_Console.png)

## Quickstart

To make sure your ssh and hosts setup is correct and you can login to all 
required servers:

```console
ansible all -m ping -i hosts
```

To install basic Linux tools (curl, vim etc.) on all servers:

```console
ansible-playbook basics.yml -i hosts
```

To install consul server and clients:

```console
ansible-playbook bootstrap.yml -i hosts
```