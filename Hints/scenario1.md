## Base Config
5A. YAML syntax can be confusing.  Look at the two lines under the "hosts:" indentation, and refer to https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html if needed.

6A & 6B. Look at line 4.  Are we trying to configure web servers in the webServers group, or DBServers?

6C. The other DevOps Engineers named everything well, so there's no need for comments!

6D. Look at the text directly under "- name:".


## Splunk Config

1A & 1B. Look at like 4, and compare that to the inventory.yml file.

1C. The other DevOps Engineers named everything well, so there's no need for comments!

1D. Look at the text directly under "- name:".  become_user is not a module.

2A. Didn't we add that SSH key when we ran that base config playbook?

3A. It should be listed if you click "host" under "SELECTED FIELDS".

3B. Look at what the source value is for each event.

3C. Didn't we update some packages, and install some packages earlier?
