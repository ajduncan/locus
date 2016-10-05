# locus #

A set of common ansible plays for servers.

## Setup ##

  1. The host needs the latest version of ansible, and python2 installed to run
  plays:

  $ cd /path/to/devops/locus
  $ git clone ...
  $ virtualenv -p python .env2
  $ source .env2/bin/activate
  (.env2) $ pip install ansible

  If there are additional requirements:

  $ pip install -r requirements.txt

  You may have luck using Ansible 2.x on Ubuntu >= 16.04.

  2. Use pass to manage encrypted passwords for host files.

    * Ubuntu/Debian: apt-get install pass
    * OSX: brew install pass

## Running ##

1. First ensure you have the proper requirements (ansible on the host) and the
proper virtual environment:

  $ cd /path/to/devops/locus
  $ source .env2/bin/activate

2. Provided you have a hosts file and ansible installed:

  $ ansible-playbook -u <user> --ask-become-pass -v main.yml --check
  $ ansible-playbook -u <user> --ask-become-pass -v main.yml --inventory-file=hosts

  Or to run against a specific host group, e.g. work:

  $ ansible-playbook -u <user> --ask-become-pass -v main.yml --inventory-file=hosts -l work

## Testing ##

  * To run a check only play:

    $ cd /path/to/devops/locus
    $ source .env2/bin/activate
    $ ansible-playbook -i hosts ./playbooks/update_host.yaml --ask-become-pass --check

  * To run against a different server group:

    ansible-playbook -i dev_hosts playbook.yaml

## Vault ##

Suppose you have an encrypted secrets.yml file, and a host file which references
username and password pairs (for become root work) that looks like:

neuro ansible_ssh_host=neuro ansible_user="{{ neuro['username'] }}" ansible_connection=ssh ansible_become_user=root ansible_become_pass="{{ neuro['password'] }}"

You can edit and encrypt an example secrets.yml file with the variables above;

neuro:
  username: 'foo'
  password: 'bar'

To run a playbook that references encrypted files, if you don't want to store
the vault password on disk, use:

  $ ansible-playbook -i hosts -v ./playbooks/update_host.yml --ask-vault-pass

and keep the vault password (for example) in LastPass or OnePassword
