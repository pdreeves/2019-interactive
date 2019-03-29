5A:

  ansible web2 -i inventory.yml -a "hostname" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  ansible web2 -i inventory.yml -a "/usr/sbin/ifconfig" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  ansible web2 -i inventory.yml -a "cat /etc/passwd" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  ansible web2 -i inventory.yml -a "yum list installed" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

5B:
  ansible webServers -i inventory.yml -a "hostname" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  ansible webServers -i inventory.yml -a "/usr/sbin/ifconfig" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  ansible webServers -i inventory.yml -a "cat /etc/passwd" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'

  ansible webServers -i inventory.yml -a "yum list installed" --extra-vars '{ "ansible_ssh_private_key_file":"sshKeyPair/interactive"}'
