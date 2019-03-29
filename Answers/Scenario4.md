# Scenario 4: Server Hardening

## Server Hardening

1A. iptables

1B. 22 from 172.17.0.0/16, and 80 from everywhere.  It is a webserver for Dr. Nick after all!

2A. Change the host on line 4 from web1 to web2

2B. Add the following task in:
- name: Allow Access to Website
  iptables:
    chain: INPUT
    source: 0.0.0.0/0
    destination_port: 443
    protocol: tcp
    jump: ACCEPT

3A. Add another task:
- name: Remove backdoor user
  user:
    name: backdoor
    state: absent

3B. Change 'web1' on line 4 to 'webServers'

4A. Since the user account was already removed in step 3, that task didn't change anything.
