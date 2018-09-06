# HyperFlex OpenShift 3.10 Install Automation w/ Ansible

## I. PRE-REQUISITES:

### A. Enable Persistent Volumes in HX Connect

### B. DNS Server Configuration:
1. All Openshift nodes that will be provisioned should be configured and resolveable in DNS prior to running ansible playbooks
    
### C. Ansible Host: (host from which ansible playbooks will be run)
- Required Software Packages:
    - ansible >= v2.6
    - pyhton >= v2.6
    - PyVmomi (for deployment of OpenShift nodes)
    - openshift-ansible 3.10.x
- Required Configuration:
    - must have SSH RSA public key generated as "~/.ssh/id_rsa.pub" (playbooks will copy public key to deployed nodes for passwordless SSH)
    - must be configured to use DNS server with hostname to IP resolution for all intended hosts

### D. Template VM
  - this VM will be used to clone the OpenShift nodes.
  - create a VM with at least 4 vCPU, 16GB RAM and two Hard Disks [1st @ 150GB and 2nd @ 40 GB]
  - only a signle interface is needed, playbook will add additional interface for HX iSCSI PV traffic
  - install RHEL 7.x accepting defaults, only providing root password during installation
    
## II. USE
