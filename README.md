# config-as-code
Configuration as code using tools such as Ansible

## Sample ansible and ansible-playbook commands

- `ansible -i inventory -v -m ping all --user user_name -v`
- `ansible-playbook -i inventory --user user_name playbooks/debian-basic.yml --ask-become-pass -v`
