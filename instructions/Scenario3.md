# Scenario 3: Inventory (and Ad-Hoc Commands)

Ansible also supports ad-hoc commands that can be run outside of a playbook.  These can be useful when you only need to run a command once, but across multiple servers.  In this section we'll use the command module to run shell commands on the servers.  Let's try ad-hoc commands out by gathering some information about our servers!

You're security department is doing an audit of server configurations.  They need to know hostnames, IP addresses, user accounts, firewall rules, and packages installed for all servers.  Normally this would be tedius, but with Ansible it's much easier.  Let's try ad-hoc commands out by gathering some information about our servers!

_Hints for this scenario are located in the scenario3.md file in the Hints folder, answers in the scenario3.md file in the Answers folder, and completed commands in the completedScenarios folder._

## Inventory
1. Get the hostname for web1:

  ansible web1 -i inventory.yml -a "hostname" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  **A. What is this server's hostname?"**

2. Get the network information for the server:

  ansible web1 -i inventory.yml -a "/usr/sbin/ifconfig" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  **A. What is the IP address of the container?**

3. Get a list of all user accounts on the server:

  ansible web1 -i inventory.yml -a "cat /etc/passwd" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  **A. Are there any user accounts that shouldn't be there?**

4. Get a list of all the packages installed on the server:

  ansible web1 -i inventory.yml -a "yum list installed" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  **A. Do you see iptables or firewalld, 2 common Linux firewall programs, in that list?**

5. We also need to gather this same information for web2.

  **A. What needs to be changed in the above commands to get the information from web2?**

  **B. What needs to be changed in the above commands to get information from both web1 and web2?**
