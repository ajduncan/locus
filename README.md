# locus #

A set of common ansible plays for servers.

## Running ##

Provided you have a hosts file and ansible installed:

    $ ansible-playbook -u <user> --ask-sudo-pass -v main.yml --check
    $ ansible-playbook -u <user> --ask-sudo-pass -v main.yml --inventory-file=hosts

