Ansible Role: Docker Swarm
==========================

Heavily modified version of [this repository](https://github.com/atosatto/ansible-dockerswarm). I've removed anything that didn't
specifically apply to my build of a Raspi swarm cluster. I will only supply
limited support.

Setup a Docker Swarm cluster on Raspberry Pi
using the new Docker Engine's "Swarm Mode" (https://docs.docker.com/engine/swarm/).

Requirements
------------

[Hypriot Raspberry Pi image](https://blog.hypriot.com/)
Three Raspberry Pis with SSH enabled, and the hostnames swarm-1, swarm-2, and swarm-3


Usage
-----

Start by generating SSH keys if you haven't already.

    ssh-keygen

Copy keys to your to-be swarm cluster. The password is 'hypriot' by default.

    ssh-copy-id pirate@swarm-1
    ssh-copy-id pirate@swarm-2
    ssh-copy-id pirate@swarm-3

Finally, run the command to configure your swarm cluster:

    ansible-playbook dockerswarm.yml -b -i hosts

Dependencies
------------

None.

Example Playbook
----------------

    $ cat hosts

    [docker_engine]
    swarm-1 ansible_user=pirate
    swarm-2 ansible_user=pirate
    swarm-3 ansible_user=pirate

    [docker_swarm_manager]
    swarm-1

    [docker_swarm_worker]
    swarm-2
    swarm-3

    $ cat playbook.yml
    - name: "Provision Docker Swarm Cluster"
      hosts: all
      roles:
        - { role: dockerswarm }

License
-------

MIT

Author Information
------------------

Original Author:
Andrea Tosatto ([@\_hilbert\_](https://twitter.com/_hilbert_))

Modified heavily by:
[John Barney](https://github.com/johnbarney)
