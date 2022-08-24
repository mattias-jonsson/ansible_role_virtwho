Ansible Role: ansible_role_pti_virtwho
=========

Installs and configures virt-who on the following Linux distributions:

<ul>
<li>Red Hat Enterprise Linux 8
</ul>

Requirements
------------

None.


Role Variables
--------------

Available variables are listed below, along with default values where applicable (see `defaults/main.yml`):

    no_proxy:

Boolean variable, set this to True to override any proxy settings that otherwise might get inhertides from OS.

    http_proxy:

Set proxy if needed.

   name:

Name of configuration, could be name of vCenter

    type:

Set to type of environment, valid values are: `libvirt`, `esx`, `hyperv`, `kubevirt`

    server:

Hostname, IP address or URL of the server that provides virtualization information. 

    username:

Username for authentication to the server. May include domain. Do not escape the backslash between domain and username. 

    password:

Password for authentication to the server. The password will be encrypted in the configuration file.

    owner:

Owner for use with Subscription Asset Manager, the Red Hat Customer Portal, or Satellite 6.

    env:

Environment for use with Subscription Asset Manager or Satellite 6.

    hypervisor_id: uuid

Property that should be used as identification of the hypervisor. Can be one of following: `uuid`, `hostname`, `hwuuid`.

    exclude_hosts:

Hosts which uuid (or hostname or hwuuid, based on hypervisor_id) is specified in comma-separated list in this option will NOT be reported.

    filter_hosts:

Only hosts which uuid (or hostname or hwuuid, based on hypervisor_id) is specified in comma-separated list in this option will be reported.

    kubeconfig:

Path to Kubernetes configuration file which contains authentication and connection details. Used by kubevirt option

    kubeversion:

API version used to override kubevirt api version fetched from the cluster. Used by kubevirt option.

Dependencies
------------

None.

Example Playbook
----------------


    - hosts: servers

      vars:
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

      roles:
         - ansible_role_virtwho

License
-------

MIT

Author Information
------------------

Mattias Jonsson
