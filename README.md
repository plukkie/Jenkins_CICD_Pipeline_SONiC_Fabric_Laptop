# Jenkins_CICD_Pipeline_SONiC_Fabric_Laptop

NOTE  
- This repo works in conjunction with repo: https://github.com/plukkie/Ansible_SONiC_EVPN_Fabric_Laptop.git
- fabric type can be : "mclag" or "evpnmh"
- The leaf and spine count in the settings.json file should have same amount of entried in the hosts file of Ansible git:  
  github.com/plukkie/Ansible_SONiC_EVPN_Fabric_Laptop/hosts  
  Else you get errors when you run the playbook: 'create_day1_playbook.yaml'  

EXAMPLE
Jenkins_CICD_Pipeline_SONiC_Fabric_Laptop/settings.json:
"gns3"	: {
		<<SNIP>>
		"nodesdata"	: {
			"posshift"  : 150,
			"templates" : {
				"leaf"	: { 
					"name"  : "DES_4.2.0", 
					"count" : 2,     <<<<<<<<<<
					<<SNIP>>
				},
				"spine" : {
					"name"  : "DES_4.2.0",
					"count" : 3,     <<<<<<<<<<<
					<<SNIP>>
				},

Change file Ansible_SONiC_EVPN_Fabric_Laptop/hosts:
sonic-SPINE-1 ansible_host=192.168.1.21
sonic-SPINE-2 ansible_host=192.168.1.22
sonic-SPINE-3 ansible_host=192.168.1.23
#sonic-SPINE-4 ansible_host=192.168.1.24
sonic-LEAF-1 ansible_host=192.168.1.11
sonic-LEAF-2 ansible_host=192.168.1.12
#sonic-LEAF-3 ansible_host=192.168.1.13
#sonic-LEAF-4 ansible_host=192.168.1.14
##sonic-LEAF-5 ansible_host=192.168.1.15
#sonic-LEAF-6 ansible_host=192.168.1.16

[spine]
sonic-SPINE-1
sonic-SPINE-2
sonic-SPINE-3
#sonic-SPINE-4

[leaf]
sonic-LEAF-1
sonic-LEAF-2
#sonic-LEAF-3
#sonic-LEAF-4
#sonic-LEAF-5
#sonic-LEAF-6

[all:children]
spine
leaf
