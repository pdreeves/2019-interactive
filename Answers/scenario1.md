## Base Config
5A. web1, and web2

6A. The group named DBServers.

6B. The hosts need to be changed from DBServers to webServers

6C. This playbook will add the EPEL repo if needed, install any available updates, add the developer account if needed, add the ssh key to the server if needed, and make sure the hostname is set correctly.

6D. yum, user, authorized_key, and hostname

## Splunk Config
1A. All hosts

1B. This is configured to run on all hosts, so there's no need to update it.

1C. Download the Splunk rpm (Linux installer package) file, run it, configure the default username and password, for Splunk, change the permissions recursively for the /opt/splunkforwarder folder, start Splunk while accepting the license, verify that the file with the username and password is removed, configure the Splunk outputs.conf file so that data is sent to the Splunk server, configure Splunk to bring in data from the yum.log file, change some permissions for Splunk to read files correctly, and restart the Splunk Universal Forwarder to re-load these changes.

1D. get_url, yum, ini_file, file, command, blockinfile, acl

2A. Since we added the ssh key in the base config, we're instructing Ansible to use that for authentication instead of promting and using a password.

3A. It should be three: web1, web2, and the splunk container itself.

3B. The /var/log/yum.log files for web1 and web2.

3C. We updated packages and installed screen, and tcpdump in the base config playbook, then installed the splunkforwarder.
