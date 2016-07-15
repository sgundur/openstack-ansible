OpenStack-Ansible
#################

OpenStack-Ansible is an `official OpenStack project`_ which aims to deploy
production environments from source in a way that makes it scalable while
also being simple to operate, upgrade, and grow.

For an overview of the mission, repositories and related Wiki home page,
please see the formal `Home Page`_ for the project.

For those looking to test OpenStack-Ansible using an All-In-One (AIO) build,
please see the `Quick Start`_ guide.

For more detailed Installation and Operator documentation, please see the
`Install Guide`_.

If OpenStack-Ansible is missing something you'd like to see included, then
we encourage you to see the `Developer Documentation`_ for more details on
how you can get involved.

Developers wishing to work on the OpenStack-Ansible project should always
base their work on the latest code, available from the master GIT repository
at `Source`_.

If you have some questions, or would like some assistance with achieving your
goals, then please feel free to reach out to us on the
`OpenStack Mailing Lists`_ (particularly openstack-operators or openstack-dev)
or on IRC in ``#openstack-ansible`` on the `freenode network`_.


**********************************************************************
How to install OpenStack - Swift+Keystone services in an AIO using OSA
**********************************************************************
        1. # apt-get update

	2. # apt-get upgrade

	3. # reboot

	4. # apt-get install git

        5. # git clone -b swift_only  https://github.com/sgundur/openstack-ansible.git /opt/openstack-ansible

        6. /opt/openstack-ansible# scripts/bootstrap-ansible.sh

        7. /opt/openstack-ansible# scripts/bootstrap-aio.sh

	8. /opt/openstack-ansible/playbooks# openstack-ansible setup-hosts.yml

        9. /opt/openstack-ansible/playbooks# openstack-ansible setup-infrastructure.yml

        10. /opt/openstack-ansible/playbooks# openstack-ansible setup-openstack.yml


--------------------------------------
Changes made, in swift_only git branch
--------------------------------------

        - In  /opt/openstack-ansible/ansible-role-requirements.yml; deleted all other roles ( except swift , keystone and utilities ) , check in /etc/ansible/roles#

	- In /openstack-ansible/etc/openstack_deploy/openstack_user_config.yml.aio; removed other networks , except br-mgmt and br-storage ; also removed other services from group_binds in br-storage ; kept only swift_proxy, remove other \*_hosts

	- Edited playbooks/setup-openstack.yml

	- Inside the /opt/openstack-ansible/etc/openstack_deploy/env.d ; deleted other \*.yml files

	- Edited /openstack-ansible/tests/roles/bootstrap-host/tasks/prepare_aio_config.yml

	- /openstack-ansible/tests/roles/bootstrap-host/defaults/main.yml ;set cinder and nova , loop back device to false)

        - Edited /openstack-ansible/tests/roles/bootstrap-host/templates/user_variables.aio.yml.j2 ; set swift_ceilometer_enabled: false


.. _official OpenStack project: http://governance.openstack.org/reference/projects/index.html
.. _Home Page: http://governance.openstack.org/reference/projects/openstackansible.html
.. _Install Guide: http://docs.openstack.org/developer/openstack-ansible/install-guide/index.html
.. _Quick Start: http://docs.openstack.org/developer/openstack-ansible/developer-docs/quickstart-aio.html
.. _Developer Documentation: http://docs.openstack.org/developer/openstack-ansible/developer-docs/index.html
.. _Source: http://git.openstack.org/cgit/openstack/openstack-ansible
.. _OpenStack Mailing Lists: http://lists.openstack.org/
.. _freenode network: https://freenode.net/
