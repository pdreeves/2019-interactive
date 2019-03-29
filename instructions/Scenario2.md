# Scenario 2: Web Server Configuration

Now that our servers are updated, configured, and sending data to Splunk it's time to get them set up to be web servers.

_Hints for this scenario are located in the scenario2.md file in the Hints folder, answers in the scenario2.md file in the Answers folder, and completed Ansible playbooks in the completedScenarios folder._

## Web Server Config

1. Confiure web1:

  ansible-playbook -i inventory.yml scenarios/scenario2-playbook-web1.yml --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  **A.It looks like we're adding a package using the yum module.  What is it?**

  **B.Why are we specifying that httpd should be restarted?**

  **C. What other sources are we ingesting in to Splunk?**

2. Let's make sure the web server is running by going to http://localhost:81 .

3. Let's also make sure Splunk is setting those logs
  1. Go to http://localhost:8000 again
  2. Execute a search of "index=web sourcetype=access_common"

  **A. What is the source IP of the requests?**

  **B. What is the user agent of the requests?**

  3. Refresh the site a few times, then run that search again to see the new logs come in.
