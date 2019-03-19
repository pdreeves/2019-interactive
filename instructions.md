
# 1 week before lab:
1. Download and install Docker CE
2. docker container run hello-world: you should see a message like this...

# Set up environment
1. Start web server containers
docker container run --detach --privileged --hostname web1 --name web1 --interactive --tty --publish 80:81 --volume /sys/fs/cgroup:/sys/fs/cgroup:ro pdreeves/2019-interactive-web

2. docker container run --detach --privileged --hostname web2 --name web2 --interactive --tty --publish 80:82 --volume /sys/fs/cgroup:/sys/fs/cgroup:ro pdreeves/2019-interactive-web

3. Start Splunk container
docker container run --detach --hostname splunk --name splunk-docker --interactive --tty --publish 8000:8000 --env SPLUNK_PASSWORD="newSplunkPassword" pdreeves/splunk-docker

4. Start Ansible host container
docker container run --detach --link=web1 --link=web2 --hostname ansible --name ansible --interactive --tty  --volume /Users:/opt/external pdreeves/2019-interactive-ansible
