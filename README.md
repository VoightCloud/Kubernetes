# Kubernetes Setup
### This is the top layer of the Voight Home Private Cloud.

This is intended to run on a combination of Raspberry Pi and x86 nodes.

This piece sets the stage by installing the master node, flannel network, metal lb load balancer, and
the nfs-client-provisioner helm charts. 

It then joins the worker nodes.

The ansible hosts.yaml file defines 7 Raspberry Pi Ubuntu nodes (kpi1-7) and two x86 Ubuntu nodes (pepper & ugli).
If you wish to customize this for your own use, you will need to install Ubuntu on all of your nodes, change
all the necessary IP addresses, add the hostnames and IP addresses to your hosts file or DNS server, and
add your SSH ID to all your machines.

### IMPORTANT
You will also want to edit the playbook and remove the apt-sources copy. I run my own private
repo and you probably don't have access to it. You don't need a private repo. It saves
me a few seconds when I'm resetting and rebuilding my cluster during development experiments.

##To run, use the following command:
```shell script
cd ansible
ansible-playbook --vault-password-file ~/secret.txt playbook.yaml
```

###To reset your Kubernetes cluster, (hopefully you don't need to do this often), you can use the following command:
```shell script
# WARNING: The reset playbook will reboot all nodes!
cd ansible
ansible-playbook reset.yaml
```

## Recommendations
The next step is to start adding your own pods and whatnot. I recommend that you add the following:

1. HA Proxy
2. OpenLDAP
3. phpLDAPadmin (optional)
2. Jenkins