    - 9 Machines - Specs: D4s_V3 (3 Master, 3 Infra, 3 App/Compute Nodes)
    - VM OS: - 
      ** CentOS: -** publisher: Openlogic, offer: CentOS, sku: 7.5, version: Latest
      ** RHEL: -** publisher: RedHat, offer: RHEL, sku: 7.5, version: Latest
    - Internet connectivity should be enabled on each node
    - Master VM’s should be in Availability zone, Infra VM’s should be in Availability zone, Node VM’s should be in Availability set
    - Create a separate VNET for these resources and make master, infra, node subnet in that and keep all the VM’s and VNET in same resource group
    - Two Load balancers (Master and Infra) (Type – L4) are required.
    - Enable ssh login (with single ssh key) to all the VM’s
    - All VM’s should have private IP addressing only
    - Create Service Principal and share SP-Secret with contributor access
    - Create two DNS entries; one for OKD web console and other for applications. These DNS IP’s needs to be associated to master and infra LB respectively.

