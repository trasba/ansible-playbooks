# ansible-playbooks

prerequisite: ansible

``` sudo apt-get install ansible ```

run with e.g.:

ansible-playbook inst-testing-repository.yml -e "hosts_prompt=\<client\> username=\<user(default=pi)\>"

### install certbot
``` ansible-playbook inst-certbot.yml -e "hosts_prompt=localhost" ```
