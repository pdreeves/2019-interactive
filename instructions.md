
# 1 week before lab:
1. Download and install Docker CE
2. docker container run hello-world: you should see a message like this...

# Set up environment

1. Start Splunk container

docker container run --detach --hostname splunk --name splunk --interactive --tty --publish 8000:8000 --env SPLUNK_PASSWORD="interactive" 2019-interactive-splunk

2. Start web1 container

docker container run --detach --link=splunk --privileged --hostname web1 --name web1 --interactive --tty --publish 81:80 --volume /sys/fs/cgroup:/sys/fs/cgroup:ro 2019-interactive-web

3. Start web1 container

docker container run --detach --link=splunk --privileged --hostname web2 --name web2 --interactive --tty --publish 82:80 --volume /sys/fs/cgroup:/sys/fs/cgroup:ro 2019-interactive-web

4. Start Ansible host container

docker container run --detach --link=web1 --link=web2 --hostname ansible --name ansible --interactive --tty  --volume /Users:/opt/external 2019-interactive-ansible


# Scenario 1: Base Server Configuration

1. Launch your shell to the Ansible host

docker container exec --tty --interactive ansible /bin/bash

2. Verify that the Ansible host can ssh in to the web servers:

ssh web1
ssh web2

3. Navigate to the directory you cloned the git repo to: cd {{insertFilePath}}

4. Generate an SSH key

ssh-keygen -f sshKeyPair/interactive -b 2048

5. Execute the first playbook

ansible-playbook -i inventory.yml scenarios/scenario1-playbook.yml --ask-pass

# Scenario 2: Configure Web Servers

1. Execute the playbook
ansible-playbook -i inventory.yml scenarios/scenario2-playbook-web1.yml --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

# Scenario 3: Configure Web Servers

1. Execute the playbook
ansible-playbook -i inventory.yml scenarios/scenario3-playbook-web1.yml --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

# Scenario 4: Inventory and Ad-Hoc Commands

1. Run ad-hoc command to get hostname
ansible web1 -i inventory.yml -a "hostname" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

2. Run ad-hoc command to get network info
ansible web1 -i inventory.yml -a " ip route sh" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

3. Run ad-hoc command to get all users
ansible web1 -i inventory.yml -a "cat /etc/passwd" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

4. Run ad-hoc command to get packages installed
ansible web1 -i inventory.yml -a "yum list installed" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

## Useful commands
### Clear out lab
docker container stop splunk web1 web2 ansible
docker container rm splunk web1 web2 ansible

### Get shell access to different containers
Ansible: docker container exec --tty --interactive ansible /bin/bash
Splunk: docker container exec --tty --interactive splunk /bin/bash
Web1: docker container exec --tty --interactive web1 /bin/bash
Web2: docker container exec --tty --interactive web2 /bin/bash
