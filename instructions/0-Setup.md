# Setup

## Startup Instructions for Windows

We're going to get our lab environment set up.  To do that we need to...
1. Navigate to https://github.com/pdreeves/2019-interactive, click "Clone or download" on the right, then click "Download ZIP".

  _Note: you do not need to have a GitHub account created to download the file._

2. Unzip the newly downloaded file, and make note of the path for that folder.

3. Start Docker Desktop with administrative privileges if it's not already running.

## Startup Instructions for macOS and Linux
We're going to get our lab environment set up.  To do that we need to...
1. Navigate to https://github.com/pdreeves/2019-interactive, click "Clone or download" on the right, then click "Download ZIP".

  _Note: you do not need to have a GitHub account to download the file._

2. Unzip the newly downloaded file, and make note of the path for that folder.

3. Start Docker if it's not already running

4. Start the Splunk docker container bu running this command:

  docker container run --detach --hostname splunk --name splunk --interactive --tty --publish 8000:8000 --env SPLUNK_PASSWORD="interactive" pdreeves/2019-interactive-splunk

5. Start our first webserver, named web1, which will listen on localhost:81:

  docker container run --detach --link=splunk --privileged --hostname web1 --name web1 --interactive --tty --publish 81:80 --volume /sys/fs/cgroup:/sys/fs/cgroup:ro pdreeves/2019-interactive-web

6. Start our second webserver, named web2, which will listen on localhost:82:

  docker container run --detach --link=splunk --privileged --hostname web2 --name web2 --interactive --tty --publish 82:80 --volume /sys/fs/cgroup:/sys/fs/cgroup:ro pdreeves/2019-interactive-web

7. Start our Ansible server, named ansible, and replace {{unzippedFolder}} with the location of the unzipped folder:

  docker container run --detach --link=web1 --link=web2 --hostname ansible --name ansible --interactive --tty  --volume {{unzippedFolder}}:/opt/external pdreeves/2019-interactive-ansible

  _For example, if I unzipped the folder in /Users/pdreeves/Downloads/2019-interactive-master the command would be..._
  docker container run --detach --link=web1 --link=web2 --hostname ansible --name ansible --interactive --tty  --volume /Users/pdreeves/Downloads/2019-interactive-master:/opt/external pdreeves/2019-interactive-ansible


## Reset Instructions for macOS
It's ok if you make a mistake and need to re-set the lab, that's the great thing about containers!

1. Run these commands to stop and delete the containers:

  docker container stop ansible web2 web1 splunk

  docker container rm ansible web2 web1 splunk

2. Then these commands to spin up fresh containers:

  docker container run --detach --hostname splunk --name splunk --interactive --tty --publish 8000:8000 --env SPLUNK_PASSWORD="interactive" 2019-interactive-splunk

  docker container run --detach --link=splunk --privileged --hostname web1 --name web1 --interactive --tty --publish 81:80 --volume /sys/fs/cgroup:/sys/fs/cgroup:ro 2019-interactive-web

  docker container run --detach --link=splunk --privileged --hostname web2 --name web2 --interactive --tty --publish 82:80 --volume /sys/fs/cgroup:/sys/fs/cgroup:ro 2019-interactive-web

  docker container run --detach --link=web1 --link=web2 --hostname ansible --name ansible --interactive --tty  --volume {{unzippedFolder}}:/opt/external 2019-interactive-ansibl
