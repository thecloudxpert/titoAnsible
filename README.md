# TiTO Ansible

This repository contains two Ansible playbooks which can be used to install the [Time Tracking Overview (TiTO) application](https://github.com/vmeoc/Tito).

This configuration builds on from a previous usecase of using Ansible with no central server. It assumes the setting up of Cloud Zone, Templates, Flavor\ Image Mapping and Network Profile is complete as described in [titoAnsibleHeadless repository](https://github.com/darrylcauldwell/titoAnsibleHeadless).

## Ansible Server Blueprint

This very simple blueprint simply deploys the VM template which contains Ansible with a a static IP address. There is no specific need for static IP here,  but I am using a static IP address as I am using a static DNS record.

As well as configuring network this generates a SSH authorization key which we can add to each Ansible client to create a simple security context server->client.

## Ansible Client Blueprint

This is a simple blueprint simply deploys the VM template. This uses an input parameter of SSH authorization key and uses cloud-init to create a user called 'ansible' which can be remotely called from Ansible server.

## Test Communications

If we deploy the Ansible Server then connect via SSH and type the public key string to screen.

```
cat /var/ansible-clients.pub
```

We can copy this from SSH session and paste as input to Ansible Client blueprint.

If all is good then when the Ansible Client blueprint is deployed you should be able to SSH to it from Ansible server without password and have sudo rights.

```
ssh ansible@<ansible-client-ip>
sudo yum update
```
