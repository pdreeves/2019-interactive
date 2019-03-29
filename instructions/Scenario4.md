# Scenario 4: Server Hardening

The security department found a few things wrong with the servers, and they'd like you to make some changes.

_Hints for this scenario are located in the scenario4.md file in the Hints folder, answers in the scenario4.md file in the Answers folder, and completed Ansible playbooks in the completedScenarios folder._

## Server Hardening

1. The first thing that needs to change is to install and configure a firewall.  Run this Ansible playbook for web1:

  ansible-playbook -i inventory.yml scenarios/scenario4-playbook-web1-firewall.yml --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  **A. Did we go with iptables or firewalld?**

  **B. What ports were opened and from what subnets?**

2. We need to do the same thing for web2, but also allow port 443.  Start with the scenario4-playbook-web2-firewall.yml file, which is a copy of the one for web1.

  **A. What do we need to change to have this run on web2?**

  **B. What needs to be added to port 443 is also allowed through?**

3. The security office discovered two user accounts that shouldn't exist.  They helped you get started by giving you a playbook to run so it removes the 'secret' user on web1:

  ansible-playbook -i inventory.yml scenarios/scenario4-playbook-user.yml --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  **A. What needs to be changed so this removes both the 'secret' and 'backdoor' accounts?**

  **B. What needs to be changed so it removes the user accounts on both servers with a single playbook?**

4. Make the required changes to that playbook, then re-run it.

  **A. Why is the text for web1 under "Remove secret user" green and not yellow?**

5. The security office also discovered some unwanted packages on the servers, specifically telnet-server, and tftp-server.  How can you remove those packages?  They did not give you anything to start working with this time.
  1. Start by creating a file named scenario4-playbook-packages.yml in the scenarios folder.
  2. Let's work on having this playbook only run on web1, and only remove telnet-server for now. (There is a hint for this.)
  3. Add in a task to use the module that will add/remove packages. (There's also a hint for this.)
  4. Run it:
    ansible-playbook -i inventory.yml scenarios/scenario4-playbook-web1-packages.yml --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

6. Let's modify the playbook you created to run on all servers, and make sure both tftp-server and telnet-server are removed.
  1. Duplicate the previously created playbook and name it
  2. Change it so it will run on all webServers (There's a hint for this.)
  3. Add another task in to also remove tftp-server.
  4. Run it:
    ansible-playbook -i inventory.yml scenarios/scenario4-playbook-packages.yml --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'
