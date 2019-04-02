# Scenario 1: Base Server Configuration

As the new DevOps Engineer at Guardian Consulting Services LLC, you've been asked to provision two new webservers.  The good news is that another DevOps Engineer already has Ansible playbooks written for this purpose, and you'll just need to execute them after updating them to run on our web servers.

 _Hints for this scenario are located in the scenario1.md file in the Hints folder, answers in the scenario1.md file in the Answers folder, and completed Ansible playbooks in the completedScenarios folder._

## Base Config
We'll need to modify and execute the base server config by...

1. Creating a shell connection (bash) to your Ansible server:

  docker container exec --tty --interactive ansible /bin/bash

2. Navigating to the folder that has the Ansible playbooks:

  cd /opt/external

3. Verifying that the Ansible server can ssh in to the servers:

  ssh web1
  ssh web2

  Accept the SSH key by typing 'yes' and hitting return, but use CTRL + C to stop the command.  _We won't be logging in to them this way, we're only testing network connectivity._

4. Generate the SSH key that will be used for password-less login to these servers for the rest of the lab:

  ssh-keygen -f sshKeyPair/interactive -b 2048

  _There's no need to have a passphrase on this key since this will just be used for the lab._

5. The inventory.yml file has a complete inventory for the web servers.

  **A. What hosts are in there?**

5. Look at the file in the scenarios folder named scenario1-playbook-base.yml.

  **A. What hosts is it going to run on?**

  **B. What needs to be updated for this playbook to run on our web servers?**

  **C. What does it look like this playbook will do?**

  **D. What Ansible modules is it using?**

6. Make the required change so that the playbook runs on the web servers, then execute the base Ansible playbook:

  ansible-playbook -i inventory.yml scenarios/scenario1-playbook-base.yml --ask-pass

  _The password is 'interactive'._

## Splunk Config
Now that the base configuration is installed we want to install and configure the Splunk Universal Forwarder (agent) to send data to Splunk.

1. Look at the file in the scenarios folder named scenario1-playbook-splunk.yml.

  **A. What hosts is it going to run on?**

  **B. Why doesn't the hosts field need to be updated?**

  **C. What does it look like this playbook will do?**

  **D. What Ansible modules is it using?**

2. Execute the Ansible playbook to configure the Splunk Universal Forwarder:

  ansible-playbook -i inventory.yml scenarios/scenario1-playbook-splunk.yml --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  **A. Why don't we have to specify the password this time?**

3. Let's make sure that Splunk is receiving the data.  
  1. Open up a web browser and go to http://localhost:8000, then log in with a username of 'admin' and password of 'interactive'.
  2. Click either "Skip" or "Ok" if prompted.
  3. Click "Search & Reporting" on the left.
  4. Click "Skip" if prompted.
  5. Run a search of "index=_*" to show the Splunk inernal logs.  You should see "host 3" on the left under "SELECTED FIELDS".

  **A. What hosts are sending in data?**

  6. Something more valuable may be running a search of "index=linux".

  **B. Where are these log files from?**

  **C. Why are those events there?**
