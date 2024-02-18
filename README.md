# config-as-code
Configuration as code using tools such as Ansible

## Prerequisites 

### Python

Both the control node and managed nodes require Python.

I like to use Python virtual environments. Create one for Ansible.

Note: If you have an old version of Python and the following does not find venv, you will need to first install the venv.

- `cd ~`
- `mkdir pyenv`
- `cd pyenv`
- `python3 -m venv pyenv/ansible`

### Ansible

Install Python in virtual environment.

- `cd ~`
- `source pyenv/ansible/bin/activate` 
- `python3 -m pip install ansible`

### SSH

You must be able to login to managed nodes using SSH. This even includes for working with localhost. Passwordless SSH is required for fully autonomous configuration. Can add a passphrase to your SSH key when you generate it for added security.

## Running against localhost

This includes the steps to get this running on the control node. This can also be useful if you want to perform some of the basic setup on a new machine. For example, if you want to setup the firewall right away.

- `cd ~`
- `source pyenv/ansible/bin/activate` 
- `mkdir ansible_projects`
- `cd ansible_projects`
- `git clone https://github.com/inertiaBill/config-as-code.git`


Notes on running playbooks,
- Current user needs sudo permission.
- Modern Linux strongly encourages login with SSH keys. If you want to use passwords rather than keys, you will need to,
    - Install sshpass.
    - Append `--ask-pass` to the following command line. 
- If you are configured to prompt for password for sudo then append `--ask-become-pass -v` to the following,

Setup ufw on localhost,
- `ansible-playbook --inventory localhost, playbooks/ufw.yml -vv`

Run linux-setup.yml use user "user_name" and ask for user_name's password,
- `ansible-playbook --inventory localhost, --user user_name playbooks/debian_common.yml --ask-become-pass -v`

## Sample ansible and ansible-playbook commands using inventory

- `ansible --inventory inventory -m ping all --user user_name -v`
- `ansible-playbook --inventory inventory --user user_name playbooks/linux_common.yml --ask-become-pass -v`
