# Scenario 2: Web Server Configuration

## Web Server Config
1A. httpd

1B. Since Ansible is idempotent, we specify the desired end-state of the task, not necessarily how to execute it.

1C. /var/log/httpd/error_log, and /var/log/httpd/access_log

2A. It's probably 172.17.0.1, but may be different if you have a custom docker network set up.

2B. It should be the browser you used to access the site.

3A. Change "web1" to "web2" on line 4.

3B. Change "web1" to "web2" on line 16.
