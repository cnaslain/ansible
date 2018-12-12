Forked from Jerome Penekuzu Ansible workshop

Install prerequisites (on a Windows workstation):
- Download and install Vagrant from https://www.vagrantup.com/downloads.html
- Download and install VirtualBox from https://www.virtualbox.org/wiki/Downloads

Clone this repo; and cd into it.

Pop up CentOS VMs (usr/pwd for all these VMs are vagrant/vagrant):

    vagrant up

Login into the 1rst VM:

    ssh vagrant@192.168.100.100
    
... and install Ansible using Yum commands (see install-ansible.txt file):

    sudo yum -y install epel-release
    sudo yum -y install ansible

The run ansible commands and playbooks.

    cd /vagrant/tp-roles
    ansible-playbook -i hosts.yaml site.yaml -u vagrant -k -b -K

Other commands executed during the workshop (from .bash_history file; some may be wrong commands!):

    ansible-playbook -i inventory test.yml -u vagrant
    ansible-playbook -i inventory test.yml -c local
    ansible-playbook -i inventory test.yml -c local -b 
    ansible-playbook -i hosts.yaml site.yaml -u vagrant -k -b -K -vvv
    
    ansible localhost -m setup -a "filter=*family*" -c local
    ansible -i roles/webserver/tests/inventory -m setup -a "filter=*family*"
    ansible -i roles/webserver/tests/inventory -m setup -a "filter=*family*" 192.168.100.200
    ansible -i roles/webserver/tests/inventory -m setup -a "filter=*family*" -u ansible 192.168.100.200
    ansible -i hosts.yaml -m setup -a "filter=*family*" 192.168.100.200
    ansible -i hosts.yaml -m setup -a "filter=*family*" 192.168.100.200 -u ansible
    ansible -i hosts.yaml -m setup -a "filter=*family*" 192.168.100.200 -u vagrant -k
    ansible localhost -m setup -a "filter=*family*" -c local
    
    ansible-playbook -i ../tp-roles/hosts.yaml local_action_plugin.yaml -u ansible -b
    ansible-playbook -i ../tp-roles/hosts.yaml delegate_to.yaml
    ansible-playbook ../tp-roles/hosts.yaml when-conditional.yaml 
    ansible-playbook -i ../tp-roles/hosts.yaml when-conditional.yaml 
    ansible-playbook -i ../tp-roles/hosts.yaml when-conditional-testing-mandatory-variables.yaml 
    ansible-playbook -i ../tp-roles/hosts.yaml when-conditional-testing-mandatory-variables.yaml -e directory=/tmp
    
    cd ../tp-roles/
    export EDITOR="emacs"
    ansible-vault create fichier-encrypte.txt
    ansible-vault decrypt fichier-encrypte.txt
    ansible-vault encrypt fichier-encrypte.txt
    ansible-vault decrypt fichier-encrypte.txt --vault-password-file=vault-pass-file
    ansible-vault encrypt fichier-encrypte.txt --vault-password-file=vault-pass-file
    ansible-vault rekey fichier-encrypte.txt --vault-password-file=vault-pass-file
    ansible-vault encrypt_string 'cnas' --name vault_password
    cd ../vault/
    ansible-playbook vault.yaml --ask-vault-pass
    
For AWX (https://github.com/ansible/awx), stop the VM, increase the memory up to 2Gb and restart the VM.
    
    sudo yum install -y git
    ansible-galaxy install -r roles/requirements.yml 
    ansible-playbook -i hosts awx.yaml 
    ansible-playbook -i hosts awx.yaml -u vagrant -k -b -K
    ssh vagrant@192.168.100.140
