# Kubernetes Cluster using Ansible

![CentOS 8](https://img.shields.io/badge/Tested_on-CentOS_8-green)
![Ubuntu 23.04](https://img.shields.io/badge/Tested_on-Ubuntu_23.04-orange)

This guide covers setting up a Kubernetes cluster using Ansible on CentOS 8 and Ubuntu 23.04.

## Prerequisites

- Clone the repository.
- Create multiple VMs or physical servers for one master and several worker nodes. You can use tools like Vagrant for VM creation. See an example [here](https://github.com/edib/many_vagrant_machines).
- Update the `ad_addr` in the `env_variables` file with the IP address of the Kubernetes master node.
- Run the following command to setup the Kubernetes Master node.
- Select the version Centos or Ubuntu.

```bash
ansible-playbook setup_master_node.yml
```

- Once the master node is ready, run the following command to set up the worker nodes.

```bash
ansible-playbook setup_worker_nodes.yml
```

- Once the workers have joined the cluster, run the following command to check the status of the worker nodes.

```bash
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

```bash
kubectl get nodes
```

## Additional information

- The IP addresses of the workers and masters added to the /etc/hosts file on all workers and masters as part of the `prerequisites.yml` playbook, if necessary or in case of DNS issues make sure the addresses have been added to /etc/hosts file.
