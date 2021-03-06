# Avi VMC Playbooks

The Avi VMC ansible playbooks provide the ability for day 0 provisioning as well as day 1 expansion tasks.  The provided playbooks allow for the user to 
1. Deploy a 3-node Avi Controller Cluster. `Deployment of the Avi Controller Cluster` playbook is invoked to set up a Avi Controller cluster as the first step to onboard the Avi Vantage platform into VMC compute domain.
2. Deploy Avi Service Engines into the VMC compute domain. `Create an Avi Service Engine` playbook is invoked whenever load-balancing capacity is desired.


--------------
## Requirements
--------------
**Python** and **ansible** are the base requirements that must be installed.  In addition to python and ansible, the following packages are also required.


### Python Modules
```
$ pip install pyvmomi avisdk
```
### Avisdk Ansible Role

```
$ ansible-galaxy install avinetworks.avisdk
```
### Linux package
```
$ apt install sshpass -y
$ yum install sshpass -y
```

--------------
## Usage
--------------
Each playbook has a corresponding variable file that requires user inputted data to successfully complete.  The variable files for each playbook denote whether specific variables are required are optional.  If a required variable is overlooked the playbook will fail to complete successfully.


--------------
### Deployment of the Avi Controller Cluster in the Compute Domain
--------------
```
Playbook:  vmc-ctl.yml
Variables: vmc-ctl-vars.yml
```

This playbook will deploy an Avi Controller cluster within the VMC compute domain; setting the admin password, and creating the 3-node cluster is desired (recommended.)

<br></br>

#### vmc-ctl-vars.yml


<table class="documentation-table" cellpadding="0" border="0">
    <tbody><tr>
        <th>Variable</th>
        <th>Choices/<font color="blue">Defaults</font></th>
        <th width="100%">Comments</th>
        </tr>
<tr>
<td >
<b>vcenter_hostname</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>IP or fqdn of VMC mgmt vCenter server used to deploy Avi Controller(s)</div>
</td>
</tr>

<tr>
<td >
<b>vcenter_username</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>Username to login to vCenter server</div>
</td>
</tr>

<tr>
<td >
<b>vcenter_password</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>Password used to authenticate with the vCenter server</div>
</td>
</tr>

<tr>
<td >
<b>datacenter</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><divstyle="font-size: small"><strong>Default:</strong> SDDC-Datacenter</td>
<td>
<div>The vCenter datacenter where the Avi Controller(s) will be deployed</div>
</td>
</tr>


<tr>
<td >
<b>cluster</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><divstyle="font-size: small"><strong>Default:</strong> Cluster-1</td>
<td>
<div>The vCenter esxi cluster name to deploy the Avi Controller(s)</div>
</td>
</tr>


<tr>
<td >
<b>datastore</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><divstyle="font-size: small"><strong>Default:</strong> WorkloadDatastore</td>
<td>
<div>The vCenter datastore to be used</div>
</td>
</tr>


<tr>
<td >
<b>folder</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><divstyle="font-size: small"><strong>Default:</strong> the Datacenter VM root</td>
<td>
<div>The vCenter VM folder for the Avi Controller VMs.  EX:  SDDC-Datacenter/vm/avi</div>
</td>
</tr>


<tr>
<td >
<b>ova_path</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>Local path/filename where to find the Avi Controller ova</div>
</td>
</tr>

<tr>
<td >
<b>management_network_pg</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>The network portgroup name to place the Avi Controller vNICs into</div>
</td>
</tr>


<tr>
<td >
<b>avi_admin_password</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>The password to set for the local admin account</div>
</td>
</tr>



<tr>
<td >
<b>ctl_memory_mb</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> 24576</td>
<td>
<div>The amount of memory in MB to assign to the Avi Controller(s)</div>
</td>
</tr>


<tr>
<td >
<b>ctl_num_cpus</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> 8</td>
<td>
<div>The number of vcpus to assign to the Avi Controller(s)</div>
</td>
</tr>

<tr>
<td >
<b>ctl_disk_size_gb</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> 128</td>
<td>
<div>The size of disk in GB to assign to the Avi Controller(s)</div>
</td>
</tr>


<tr>
<td >
<b>cluster_vip</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>Cluster VIP to be used for a 3 node cluster</div>
</td>
</tr>

<tr>
<td >
<b>three_node_cluster</b><br><div style="font-size: small">boolean
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><li>True</li><li>False (Default)</li></td>
<td>
<div>Deploy 3 Avi Controller nodes and cluster them</div>
</td>
</tr>


<tr>
<td >
<b>node1_mgmt_ip</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> DHCP</td>
<td>
<div>MGMT IP address to Avi Cluster node 1, if blank DHCP will be used.  <strong>Recommended to specify a static IP address</strong></div>
</td>
</tr>


<tr>
<td >
<b>node1_mgmt_mask</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> DHCP</td>
<td>
<div>Netmask to be used when static IP is assigned.  <strong>Example:</strong>  24  <strong>Recommended to specify a static IP address</strong></div>
</td>
</tr>

<tr>
<td >
<b>node1_mgmt_gw</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> DHCP</td>
<td>
<div>Gateway IP to be used when static IP is assigned.<strong>  Recommended to specify a static IP address</strong></div>
</td>
</tr>


<tr>
<td >
<b>node2_mgmt_ip</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> DHCP</td>
<td>
<div>MGMT IP address to Avi Cluster node 2, if blank DHCP will be used.  <strong>Recommended to specify a static IP address</strong></div>
</td>
</tr>


<tr>
<td >
<b>node2_mgmt_mask</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> DHCP</td>
<td>
<div>Netmask to be used when static IP is assigned.    <strong>Example:</strong>  24  <strong>Recommended to specify a static IP address</strong></div>
</td>
</tr>



<tr>
<td >
<b>node2_mgmt_gw</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> DHCP</td>
<td>
<div>Gateway IP to be used when static IP is assigned.<strong>  Recommended to specify a static IP address</strong></div>
</td>
</tr>



<tr>
<td >
<b>node3_mgmt_ip</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> DHCP</td>
<td>
<div>MGMT IP address to Avi Cluster node 3, if blank DHCP will be used.  <strong>Recommended to specify a static IP address</strong></div>
</td>
</tr>


<tr>
<td >
<b>node3_mgmt_mask</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> DHCP</td>
<td>
<div>Netmask to be used when static IP is assigned.    <strong>Example:</strong>  24  <strong>Recommended to specify a static IP address</strong></div>
</td>
</tr>



<tr>
<td >
<b>node3_mgmt_gw</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> DHCP</td>
<td>
<div>Gateway IP to be used when static IP is assigned.<strong>  Recommended to specify a static IP address</strong></div>
</td>
</tr>



</tbody>
</table>




<br></br>
--------------

--------------
### Create an Avi Service Engine in the Compute Domain
--------------
--------------
```
Playbook:  vmc-se.yml
Variables: vmc-se-vars.yml
```

This playbook will deploy Avi Service Engines within the VMC Compute  Domain.

<br></br>
#### vmc-se-vars.yml

<table class="documentation-table" cellpadding="0" border="0">
    <tbody><tr>
        <th>Variable</th>
        <th>Choices/<font color="blue">Defaults</font></th>
        <th width="100%">Comments</th>
        </tr>


<tr>
<td >
<b>avi_controller_ip</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>IP or fqdn of Avi Controller cluster for the service engine</div>
</td>
</tr>

<tr>
<td >
<b>avi_username</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>Username to use for authentication to the Avi Controller</div>
</td>
</tr>

<tr>
<td >
<b>avi_password</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>Password to use for authentication to the Avi Controller</div>
</td>
</tr>


<tr>
<td >
<b>cloud</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong>  Default-Cloud</td>
<td>
<div>Name of the Avi Cloud to deploy the Avi Service Engine in</div>
</td>
</tr>

<tr>
<td >
<b>segroup</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong>  Default-Group</td>
<td>
<div>Name of the Avi serviceengine group to deploy the Avi Service Engine in</div>
</td>
</tr>

<tr>
<td >
<b>vcenter_hostname</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>IP or fqdn of VMC compute vCenter server used to deploy Avi Service Engine</div>
</td>
</tr>

<tr>
<td >
<b>vcenter_username</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>Username to login to vCenter server</div>
</td>
</tr>

<tr>
<td >
<b>vcenter_password</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>Password used to authenticate with the vCenter server</div>
</td>
</tr>

<tr>
<td >
<b>datacenter</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><divstyle="font-size: small"><strong>Default:</strong> SDDC-Datacenter</td>
<td>
<div>The vCenter datacenter where the Avi Service Engine will be deployed</div>
</td>
</tr>


<tr>
<td >
<b>cluster</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><divstyle="font-size: small"><strong>Default:</strong> Cluster-1</td>
<td>
<div>The vCenter esxi cluster name to deploy the Service Engine</div>
</td>
</tr>


<tr>
<td >
<b>datastore</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><divstyle="font-size: small"><strong>Default:</strong> WorkloadDatastore</td>
<td>
<div>The vCenter datastore to be used</div>
</td>
</tr>


<tr>
<td >
<b>folder</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><divstyle="font-size: small">Default is the Datacenter VM root</td>
<td>
<div>The vCenter VM folder for the Avi Service Engine VM.  EX:  SDDC-Datacenter/vm/avi</div>
</td>
</tr>


<tr>
<td >
<b>management_network_pg</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>The network portgroup name to place the Avi service engine management vNIC into</div>
</td>
</tr>


<tr>
<td >
<b>data_nic_parking_pg</b><br><div style="font-size: small">string / required
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>The network portgroup name to place unused Avi service engine data vNIC(s) into</div>
</td>
</tr>

<tr>
<td >
<b>se_mgmt_ip</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> DHCP</td>
<td>
<div>MGMT IP address to assign to Service Engine, if blank DHCP will be used.  <strong>Recommended to specify a static IP address</strong></div>
</td>
</tr>


<tr>
<td >
<b>se_mgmt_mask</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> DHCP</td>
<td>
<div>Netmask to be used when static IP is assigned.    <strong>Example:</strong>  24 <strong>Recommended to specify a static IP address</strong></div>
</td>
</tr>

<tr>
<td >
<b>se_mgmt_gw</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> DHCP</td>
<td>
<div>Gateway IP to be used when static IP is assigned.<strong>  Recommended to specify a static IP address</strong></div>
</td>
</tr>



<tr>
<td >
<b>se_memory_mb</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> 4096</td>
<td>
<div>The amount of memory in MB to assign to the Avi Service Engine</div>
</td>
</tr>

<tr>
<td >
<b>se_memory_reserve_lock</b><br><div style="font-size: small">boolean
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><li>True</li><li>False - Default</li></td>
<td>
<div>Reserve service engine memory on esxi server</div>
</td>
</tr>


<tr>
<td >
<b>se_num_cpus</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> 2</td>
<td>
<div>The number of vcpus to assign to the Avi Service Engine</div>
</td>
</tr>

<tr>
<td >
<b>se_cpu_reserve_mhz</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"></td>
<td>
<div>Amount of CPU in mhz to reserve on esxi server for the Service Engine</div>
</td>
</tr>

<tr>
<td >
<b>se_disk_size_gb</b><br><div style="font-size: small">string
<div style="font-size: small">
</div>
</td>
<td><b></b><br><div style="font-size: small"><strong>Default:</strong> 20</td>
<td>
<div>The size of disk in GB to assign to the Avi Service Engine</div>
</td>
</tr>



</tbody>
</table>

<table class="documentation-table" cellpadding="0" border="0">
    <tbody><tr>

<tr>
<td colspan="2">
<b>data_network1</b>
<div style="font-size: small">
<span style="color: purple">dictionary</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Parameters for defining data vnic 1 on Avi Service Engine</div>
</td>
</tr>

<tr>
<td>
</td>
<td colspan="1">
<b>se_int_pg</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Port group name to use for SE data nic 1, leave blank for unused</div>
</td>
</tr>


<tr>
<td>
</td>
<td colspan="1">
<b>se_int_ip</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined</div>
</td>
</tr>



<tr>
<td>
</td>
<td colspan="1">
<b>se_int_mask</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined.  <strong>Example:</strong> 24</div>
</td>
</tr>

</tbody>
</table>

<table class="documentation-table" cellpadding="0" border="0">
    <tbody><tr>

<tr>
<td colspan="2">
<b>data_network2</b>
<div style="font-size: small">
<span style="color: purple">dictionary</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Parameters for defining data vnic 2 on Avi Service Engine</div>
</td>
</tr>

<tr>
<td>
</td>
<td colspan="1">
<b>se_int_pg</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Port group name to use for SE data nic 2, leave blank for unused</div>
</td>
</tr>


<tr>
<td>
</td>
<td colspan="1">
<b>se_int_ip</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined</div>
</td>
</tr>



<tr>
<td>
</td>
<td colspan="1">
<b>se_int_mask</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined.  <strong>Example:</strong> 24</div>
</td>
</tr>

</tbody>
</table>

<table class="documentation-table" cellpadding="0" border="0">
    <tbody><tr>

<tr>
<td colspan="2">
<b>data_network3</b>
<div style="font-size: small">
<span style="color: purple">dictionary</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Parameters for defining data vnic 3 on Avi Service Engine</div>
</td>
</tr>

<tr>
<td>
</td>
<td colspan="1">
<b>se_int_pg</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Port group name to use for SE data nic 3, leave blank for unused</div>
</td>
</tr>


<tr>
<td>
</td>
<td colspan="1">
<b>se_int_ip</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined</div>
</td>
</tr>



<tr>
<td>
</td>
<td colspan="1">
<b>se_int_mask</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined.  <strong>Example:</strong> 24</div>
</td>
</tr>

</tbody>
</table>


<table class="documentation-table" cellpadding="0" border="0">
    <tbody><tr>

<tr>
<td colspan="2">
<b>data_network4</b>
<div style="font-size: small">
<span style="color: purple">dictionary</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Parameters for defining data vnic 4 on Avi Service Engine</div>
</td>
</tr>

<tr>
<td>
</td>
<td colspan="1">
<b>se_int_pg</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Port group name to use for SE data nic 4, leave blank for unused</div>
</td>
</tr>


<tr>
<td>
</td>
<td colspan="1">
<b>se_int_ip</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined</div>
</td>
</tr>



<tr>
<td>
</td>
<td colspan="1">
<b>se_int_mask</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined.  <strong>Example:</strong> 24</div>
</td>
</tr>

</tbody>
</table>

<table class="documentation-table" cellpadding="0" border="0">
    <tbody><tr>

<tr>
<td colspan="2">
<b>data_network5</b>
<div style="font-size: small">
<span style="color: purple">dictionary</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Parameters for defining data vnic 5 on Avi Service Engine</div>
</td>
</tr>

<tr>
<td>
</td>
<td colspan="1">
<b>se_int_pg</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Port group name to use for SE data nic 5, leave blank for unused</div>
</td>
</tr>


<tr>
<td>
</td>
<td colspan="1">
<b>se_int_ip</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined</div>
</td>
</tr>



<tr>
<td>
</td>
<td colspan="1">
<b>se_int_mask</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined.  <strong>Example:</strong> 24</div>
</td>
</tr>

</tbody>
</table>

<table class="documentation-table" cellpadding="0" border="0">
    <tbody><tr>

<tr>
<td colspan="2">
<b>data_network6</b>
<div style="font-size: small">
<span style="color: purple">dictionary</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Parameters for defining data vnic 6 on Avi Service Engine</div>
</td>
</tr>

<tr>
<td>
</td>
<td colspan="1">
<b>se_int_pg</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Port group name to use for SE data nic 6, leave blank for unused</div>
</td>
</tr>


<tr>
<td>
</td>
<td colspan="1">
<b>se_int_ip</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined</div>
</td>
</tr>



<tr>
<td>
</td>
<td colspan="1">
<b>se_int_mask</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined.  <strong>Example:</strong> 24</div>
</td>
</tr>

</tbody>
</table>


<table class="documentation-table" cellpadding="0" border="0">
    <tbody><tr>

<tr>
<td colspan="2">
<b>data_network7</b>
<div style="font-size: small">
<span style="color: purple">dictionary</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Parameters for defining data vnic 7 on Avi Service Engine</div>
</td>
</tr>

<tr>
<td>
</td>
<td colspan="1">
<b>se_int_pg</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Port group name to use for SE data nic 7, leave blank for unused</div>
</td>
</tr>


<tr>
<td>
</td>
<td colspan="1">
<b>se_int_ip</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined</div>
</td>
</tr>



<tr>
<td>
</td>
<td colspan="1">
<b>se_int_mask</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined.  <strong>Example:</strong> 24</div>
</td>
</tr>

</tbody>
</table>




<table class="documentation-table" cellpadding="0" border="0">
    <tbody><tr>

<tr>
<td colspan="2">
<b>data_network8</b>
<div style="font-size: small">
<span style="color: purple">dictionary</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Parameters for defining data vnic 8 on Avi Service Engine</div>
</td>
</tr>

<tr>
<td>
</td>
<td colspan="1">
<b>se_int_pg</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Port group name to use for SE data nic 8, leave blank for unused</div>
</td>
</tr>


<tr>
<td>
</td>
<td colspan="1">
<b>se_int_ip</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined</div>
</td>
</tr>



<tr>
<td>
</td>
<td colspan="1">
<b>se_int_mask</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined.  <strong>Example:</strong> 24</div>
</td>
</tr>

</tbody>
</table>

<table class="documentation-table" cellpadding="0" border="0">
    <tbody><tr>

<tr>
<td colspan="2">
<b>data_network9</b>
<div style="font-size: small">
<span style="color: purple">dictionary</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Parameters for defining data vnic 9 on Avi Service Engine</div>
</td>
</tr>

<tr>
<td>
</td>
<td colspan="1">
<b>se_int_pg</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td>
</td>
<td>
<div>Port group name to use for SE data nic 9, leave blank for unused</div>
</td>
</tr>


<tr>
<td>
</td>
<td colspan="1">
<b>se_int_ip</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined</div>
</td>
</tr>



<tr>
<td>
</td>
<td colspan="1">
<b>se_int_mask</b>
<div style="font-size: small">
<span style="color: purple">string</span>                 
</div>
</td>
</div>
</td>
<td><strong><li>Default:</strong>  DHCP if se_int_pg is defined
</td>
<td>
<div>IP address to assign to data nic.  Defaults to DHCP if blank and se_int_pg is defined.  <strong>Example:</strong> 24</div>
</td>
</tr>

</tbody>
</table>
