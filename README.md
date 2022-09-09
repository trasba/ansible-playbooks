# ansible-playbooks

prerequisite: ansible

``` sudo apt-get install ansible ```

run with e.g.:

``` ansible-playbook inst-testing-repository.yml -e "hosts_prompt=\<client\> username=\<user(default=pi)\>" --ask-become-pass ```

### install certbot
Playbook will check now for architecture and version supported are now:
* Ubuntu 18.04
* Raspbian (stretch / 9)

Playbook can now be run from commandline entirely: use -e plus
* domain: (enter domain name for certificate here)
* email: (enter email to use with letsencrypt)
If the host-vars are not set the user will be prompted for them

``` ansible-playbook inst-certbot.yml -e "hosts_prompt=localhost domain=<xy.com> email=<user@xy.com>" --ask-become-pass ```

## init system
* ```ansible-playbook inst-sshkey.yml -e "hosts_prompt=<host> user=<github_user>" --ask-pass```  
this will create a ssh (ecdsa) key pair and download all public keys from the <github_user> account into the authorized_keys file on <host>
* (optional manual step) add created pub key to github  
* ```ansible-playbook sec-ssh.yml -e "hosts_prompt=<host>" --ask-become-pass```  
this will disable password, PAM, ChallengeResponse authentication
* verify this with ```ssh -o PreferredAuthentications=password -o PubkeyAuthentication=no <user>@<host>``` -> result should be ***Permission denied (publickey)***
* (optional) ```ansible-playbook inst-docker.yml -e "hosts_prompt=<host>" --ask-become-pass```  
this will install **docker** from get.docker.com and **docker-compose** via pip  
this will aslo explicitly install pip3 and update it to the newest version
* (optional) ```ansible-playbook inst-golang.yml -e "hosts_prompt=<host>"```  
this will install **golang** (v.1.16.3) according to instructions from golang.org  
this will install the version for plattform **armv6**

```
export AP_TARGET=<host>
export AP_GHUSER=<github-username>
ansible-playbook inst-sshkey.yml -e "hosts_prompt=$AP_TARGET user=$AP_GHUSER" --ask-pass && \
ansible-playbook sec-ssh.yml -e "hosts_prompt=$AP_TARGET" && \
ansible-playbook inst-docker.yml -e "hosts_prompt=$AP_TARGET" && \
ansible-playbook inst-docker.yml -e "hosts_prompt=$AP_TARGET"
```

## info on selected flags
* --ask-pass -> ask for password on connection to machine
