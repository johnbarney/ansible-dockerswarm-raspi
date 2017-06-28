Ansible Role: Docker Swarm
==========================

Heavily modified version of [this repository](https://github.com/atosatto/ansible-dockerswarm). I've removed anything that didn't
specifically apply to my build of a Raspi swarm cluster. I will only supply
limited support.

Setup a Docker Swarm cluster on Raspberry Pi
using the new Docker Engine's "Swarm Mode" (https://docs.docker.com/engine/swarm/).

Requirements
------------

* Three Raspberry Pis running Raspbian Lite with SSH enabled, and the hostnames swarm-1, swarm-2, and swarm-3
* Optional a fourth pi to run ansible from.

Usage
-----

Start by generating SSH keys if you haven't already.

    ssh-keygen

Copy keys to your to-be swarm cluster. The password is 'raspberry' by default.

    ssh-copy-id swarm-1
    ssh-copy-id swarm-2
    ssh-copy-id swarm-3

Remove password from pi account on swarm (for security, optional)

    ssh swarm-1 sudo passwd -d pi
    ssh swarm-2 sudo passwd -d pi
    ssh swarm-3 sudo passwd -d pi

Finally, run the command to configure your swarm cluster from this repo:

    ansible-playbook dockerswarm.yml -b -i hosts

Dependencies
------------

None.

Example Playbook
----------------

    $ cat hosts

    [docker_engine]
    swarm-1
    swarm-2
    swarm-3

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
