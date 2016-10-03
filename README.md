# locus #

A set of common ansible plays for servers.

## Running ##

Provided you have a hosts file and ansible installed:

    $ ansible-playbook -u <user> --ask-become-pass -v main.yml --check
    $ ansible-playbook -u <user> --ask-become-pass -v main.yml --inventory-file=hosts

Or to run against a specific host group, e.g. work:

    $ ansible-playbook -u <user> --ask-become-pass -v main.yml --inventory-file=hosts -l work
