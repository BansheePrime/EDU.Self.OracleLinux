## ...


### hard ssh check
ssh vagrant@192.168.56.19 -i ./.vagrant/machines/station/virtualbox/private_key

### check with ping
ansible -m ping -i inventory.yaml all


### check for apps
ansible-playbook -i inventory.yaml app-playbook.yaml

