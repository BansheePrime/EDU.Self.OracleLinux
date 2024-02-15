## ...


### hard ssh check
ssh vagrant@192.168.56.19 -i ./.vagrant/machines/station/virtualbox/private_key

### check with ping
ansible -m ping -i inventory.yaml all


### check for apps
ansible-playbook -i inventory.yaml app-playbook.yaml


#### tmux packager manager installation
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm


#### tmux theme installation and docs
<https://github.com/catppuccin/tmux?tab=readme-ov-file>

