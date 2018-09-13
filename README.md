# HyperFlex OpenShift 3.10 Install Automation w/ Ansible

## I. PRE-REQUISITES:

### A. Enable Persistent Volumes in HX Connect

### B. DNS Server Configuration:
1. All Openshift nodes that will be provisioned should be configured and resolveable in DNS prior to running ansible playbooks
    
### C. Ansible Host: (host from which ansible playbooks will be run)
- Should be RHEL OS
- Required Software Packages: (tested with the following)
    - ansible >= v2.6.x
    - python >= v2.7.x
    - PyVmomi >= 6.7.x (for deployment of OpenShift nodes)
    - openshift-ansible 3.10.x --> https://github.com/openshift/openshift-ansible/tree/release-3.10 --> clone repo to /usr/share/ansible/ directory.
- Required Configuration:
    - must have SSH RSA public key generated as "~/.ssh/id_rsa.pub" (playbooks will copy public key to deployed nodes for passwordless SSH)
    - must be configured to use DNS server with hostname to IP resolution for all intended hosts
    - must uncomment line "host_key_checking=False" in /etc/ansible/ansible.cfg file.

### D. Template VM
  - this VM will be used to clone the OpenShift nodes.
  - create a VM with at least 4 vCPU, 16GB RAM and two Hard Disks [1st @ 150GB and 2nd @ 40 GB]
  - only a signle interface is needed, playbook will add additional interface for HX iSCSI PV traffic
  - install RHEL 7.x accepting defaults, only providing root password during installation
  - edit the /etc/ssh/sshd_config file and set "PermitRootLogin" to "yes" on the template VM.
  - disable IPv6 --> https://www.thegeekdiary.com/centos-rhel-7-how-to-disable-ipv6/
  - install perl (required to set ip address through ansible vmware_guest module)
    
## II. EDITING THE ANSIBLE INVENTORY FILE:
  - Edit the "ocp-3.10-inventory" file and update the information based on your environment.
  
## III. RUNNING THE PLAYBOOK
  - Run `ansible-playbook -i <path-to-inventory-file> <path-to-ocp-3.10-cluster-setup.yml>`
