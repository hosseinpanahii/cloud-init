## Centos:
---
root@kvm-host1:~/images/deploy-1# vi user-data
---
#cloud-config
users:
 - name: cloud
   sudo: ['ALL=(ALL) NOPASSWD:ALL']
   ssh_authorized_keys:
     - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDRVQMsnIZPQiGEMRvNNoITuP1PRNcn38PmgH8wJOpDtxGnHI2D7fKrudk71WEC6rDb6fO8KAabmeSRbb5YyIp
   groups: users
   shell: /bin/bash
runcmd:
 - echo "AllowUsers cloud" >> /etc/ssh/sshd_config
 - restart ssh
 root@kvm-host1:~/images/deploy-1# vi meta-data
	local-hostname: deploy-1
kvm-host1:~/images/deploy-1# genisoimage -output deploy-cidata.iso -volid cidata -joliet -rock user-data meta-data
kvm-host1:~/images/deploy-1# virt-install --connect qemu:///system --virt-type kvm --name deploy-1 --ram 2048 --vcpu=1 --os-type linux --os-variant generic --disk path=/root/images/deploy-1/centos8-1.qcow2,format=qcow2 --disk /root/images/deploy-1/deploy-cidata.iso,device=cdrom --import --network network=default --noautoconsole

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------
##Ubuntu:
========

