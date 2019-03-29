# Scenario 2: Web Server Configuration

Now that our servers are updated, configured, and sending data to Splunk it's time to get them set up to be web servers.  We want web1 to show a website for Dr. Nick, and web2 to show a memorial website for Poochie.  The website file for Dr. Nick is files/web1/index.html and for Poochie is files/web2/index.html.

_Hints for this scenario are located in the scenario2.md file in the Hints folder, answers in the scenario2.md file in the Answers folder, and completed Ansible playbooks in the completedScenarios folder._

## Web Server Config

1. Configure web1:

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

3. Let's configure web2 now.  Take a look at the file scenario2-playbook-web2.yml in the scenarios folder is identical to scenario2-playbook-web1.yml.

  **A. What needs to change for this playbook to work correctly on web2?**

4. Make the changes on this playbook so it runs on web2, then run it:

  ansible-playbook -i inventory.yml scenarios/scenario2-playbook-web2.yml --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

5. Navigate to http://localhost:82 .

  **A. Are you seeing the website for Dr. Nick?  What changes do we need to make so it displays the website for the Poochie Memorial page?**

6. Make the appropriate change, then re-run the playbook.
