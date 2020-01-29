### Operating system requirements
    - For cloud-based installations, use a base installation of RHEL 7.5 or later with the latest packages from the Extras channel (Red Hat Subscription Required for extra channel repos).

### Ensuring host access
    - Confirm that you have access to each host through ssh from installer/controller machine.
```
$ ssh -i secret.pem clusteradmin@<hostname>
```

### Registering hosts
    - To access the installation packages, you must register each host with Red Hat Subscription Manager (RHSM).
```
$ subscription-manager register --username=<user_name> --password=<password>
$ subscription-manager refresh
$ subscription-manager list --available
$ subscription-manager attach --pool=<pool_id>
```

### Enable extra repos (Specific to Azure VM’s)
```
$ sudo rm /etc/yum/vars/releasever
$ yum --disablerepo='*' remove 'rhui-azure-rhel7-eus'
$ yum --config='https://rhelimage.blob.core.windows.net/repositories/rhui-microsoft-azure-rhel7.config' install 'rhui-azure-rhel7'
$ yum update
$ yum install -y  wget git zile nano net-tools docker-1.13.1 bind-utils iptables-services bridge-utils bash-completion kexec-tools sos psacct openssl-devel httpd-tools NetworkManager python-cryptography python2-pip python-devel  python-passlib java-1.8.0-openjdk-headless
$ docker version
$ systemctl enable docker
$ systemctl start docker
$ reboot
```

### Installing base packages

    -  Install epel
	```
	$ yum -y install epel-release
	```
    - Disable the EPEL repository globally so that is not accidentally used during later steps of the installation
	```
	$ sed -i -e "s/^enabled=1/enabled=0/" /etc/yum.repos.d/epel.repo

	$ systemctl | grep
		if [ $? -eq 1 ]; then
			systemctl start NetworkManager
			systemctl enable NetworkManager
		fi
	```
    - Install the packages for Ansible
	```
	$ yum -y --enablerepo=epel install pyOpenSSL

	$ curl -o ansible.rpm https://releases.ansible.com/ansible/rpm/release/epel-7-x86_64/ansible-2.6.5-1.el7.ans.noarch.rpm
	$ yum -y --enablerepo=epel install ansible.rpm
	```


### References:
OKD 3.11:- (https://docs.okd.io/3.11/install/configuring_inventory_file.html)
OCP 3.11:- (https://docs.openshift.com/container-platform/3.11/install/host_preparation.html)
