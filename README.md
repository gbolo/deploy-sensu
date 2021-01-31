# Deployment of sensu-go

## Requirements
clone this repo and cd to `ansible` directory.
To ensure you have the local requirements for your ansible host, run this playbook:
```
ansible-playbook local_python_requirements.yaml
```

You also need to install the required collections:
```
ansible-galaxy install -r required_collections.yaml
```

## Inventory
At the moment, this deployment assumes you do not want to use `sensu-backend`
embedded etcd option. As such you will need the `etcd` group populated.
Follow a similar inventory for now:
```
cat env/sensu-lab/hosts

[backend]
sensu-backend1.lab.linuxctl.com
sensu-backend2.lab.linuxctl.com

[etcd]
sensu-etcd1.lab.linuxctl.com
sensu-etcd2.lab.linuxctl.com
sensu-etcd3.lab.linuxctl.com

[agent]
sensu-agent1.lab.linuxctl.com
```

## Getting started
The playbooks and roles here will take care of the following:
- generate a new PKI for TLS (`artifacts/pki`)
- deploy an etcd cluster using the PKI
- deploy a sensu-backend cluster using the PKI
- configure the sensu-backend API with some sensu resources
- deploy the sensu-agents with basic checks

```
ansible-playbook -i env/sensu-lab playbooks_sensu/site.yaml
```
