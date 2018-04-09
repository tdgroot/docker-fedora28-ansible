# Fedora 28 Ansible Test Image

[HEAVILY INSPIRED BY JEFF GEERLING](https://github.com/geerlingguy/docker-fedora27-ansible)

Fedora 28 Docker container for Ansible playbook and role testing.

## How to Build

This image is built on Docker Hub automatically any time the upstream OS container is rebuilt, and any time a commit is made or merged to the `master` branch. But if you need to build the image on your own locally, do the following:

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. `cd` into this directory.
  3. Run `docker build -t fedora28-ansible .`

## How to Use

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. Pull this image from Docker Hub: `docker pull tdgroot/fedora28-ansible:latest` (or use the tag you built earlier, e.g. `fedora28-ansible`).
  3. Run a container from the image: `docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro tdgroot/docker-fedora28-ansible:latest /usr/lib/systemd/systemd` (to test my Ansible roles, I add in a volume mounted from the current working directory with ``--volume=`pwd`:/etc/ansible/roles/role_under_test:ro``).
  4. Use Ansible inside the container:
    a. `docker exec --tty [container_id] env TERM=xterm ansible --version`
    b. `docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check`

## Notes

I use Docker to test my Ansible roles and playbooks on multiple OSes using CI tools like Jenkins and Travis. This container allows me to test roles and playbooks using Ansible running locally inside the container.

> **Important Note**: I use this image for testing in an isolated environment—not for production—and the settings and configuration used may not be suitable for a secure and performant production environment. Use on production servers/in the wild at your own risk!

## Author

Created in 2018 by [Jeff Geerling](https://jeffgeerling.com/) and [Timon de Groot](https://github.com/tdgroot).
