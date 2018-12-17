# ansible-playbooks

prerequisite: ansible

``` sudo apt-get install ansible ```

run with e.g.:

ansible-playbook inst-testing-repository.yml -e "hosts_prompt=\<client\> username=\<user(default=pi)\>" --ask-become-pass

### install certbot
Playbook will check now for architecture and version supported are now:
* Ubuntu 18.04
* Raspbian (stretch / 9)

Playbook can now be run from commandline entirely: use -e plus
* domain: (enter domain name for certificate here)
* email: (enter email to use with letsencrypt)
If the host-vars are not set the user will be prompted for them

``` ansible-playbook inst-certbot.yml -e "hosts_prompt=localhost domain=<xy.com> email=<user@xy.com>" ```
