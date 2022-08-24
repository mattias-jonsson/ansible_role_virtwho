ansible_role_pti_virtwho
==============


This role performs the following operations on supported Red Hat Linux systems:

* Installs virt-who if missing.
* Configures virt-who through host/group variables

Requirements
---------------

Tested on:

* RHEL 8


Role variables
---------------

The following variables can be configured through host or group variables:

``` 
ansible_role_virtwho_global_config:
   no_proxy:
   http_proxy:

ansible_role_virtwho_hypervisor_config:
  - name:
    type:
    server:
    username:
    password:
    owner:
    env:
    hypervisor_id:
    exclude_hosts:
    filter_hosts:
    kubeconfig:
    kubeversion:`
```

### ansible_role_virtwho_global_config variables

* `no_proxy`

Boolean variable, set this to True to override any proxy settings that otherwise might get inhertides from OS.

* `http_proxy`

Set proxy if needed.

### ansible_role_virtwho_hypervisor_config variables

* `name`

Name of configuration, could be name of vCenter

* `type`

Set to type of environment, valid values are: **libvirt, esx, hyperv, kubevirt**

* `server`

Hostname, IP address or URL of the server that provides virtualization information. 

* `username`

Username for authentication to the server. May include domain. Do not escape the backslash between domain and username. 

* `password`

Password for authentication to the server. The password will be encrypted in the configuration file.

* `owner`

Owner for use with Subscription Asset Manager, the Red Hat Customer Portal, or Satellite 6.

* `env`

Environment for use with Subscription Asset Manager or Satellite 6.

* `hypervisor_id`

Property that should be used as identification of the hypervisor. Can be one of following: **uuid, hostname, hwuuid**. Note that some virtualization backends don't have all of them implemented. Default is uuid. hwuuid is applicable to esx and rhevm only. This property is meant to be set up before initial run of virt-who. Changing it later will result in duplicated entries in the subscription manager. 

* `exclude_hosts`


* `filter_hosts`


* `kubeconfig`


* `kubeversion`



Sample configuration
---------------

```yaml
ansible_role_virtwho_global_config:
  no_proxy: false
  http_proxy:

ansible_role_virtwho_hypervisor_config:
  - name: demo-vcenter
    type: esx
    server: demo-vcenter.localdomain
    username: demouser
    password: supersecret
    owner: 12345
    env: Customer Portal
    hypervisor_id: hostname
    exclude_hosts: vcenter-d4.localdomain
    filter_hosts:
    kubeconfig:
    kubeversion:
```