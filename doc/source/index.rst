=================================
Manila role for OpenStack-Ansible
=================================

This Ansible role installs and configures OpenStack manila.

The following manila services are managed by the role:
    * manila-api
    * manila-scheduler
    * manila-share
    * manila-data (untested)

.. toctree::
   :maxdepth: 2

   configure-manila.rst

To clone of view the source code for this repository, visit the role repository
for `os_manila <https://github.com/openstack/openstack-ansible-os_manila>`_.

Default variables
~~~~~~~~~~~~~~~~~

.. literalinclude:: ../../defaults/main.yml
   :language: yaml
   :start-after: under the License.

Dependencies
~~~~~~~~~~~~

This role needs pip >= 7.1 installed on the target host.

Example playbook
~~~~~~~~~~~~~~~~

.. literalinclude:: ../../examples/playbook.yml
   :language: yaml

External Restart Hooks
~~~~~~~~~~~~~~~~~~~~~~

When the role performs a restart of the service, it will notify an Ansible
handler named ``Manage LB``, which is a noop within this role. In the
playbook, other roles may be loaded before and after this role which will
implement Ansible handler listeners for ``Manage LB``, allowing external roles
to manage the load balancer endpoints responsible for sending traffic to the
servers being restarted by marking them in maintenance or active mode,
draining sessions, etc. For an example implementation, please reference the
`ansible-haproxy-endpoints role <https://github.com/Logan2211/ansible-haproxy-endpoints>`_
used by the openstack-ansible project.

Tags
~~~~

This role supports two tags: ``manila-install`` and ``manila-config``

The ``manila-install`` tag can be used to install and upgrade.

The ``manila-config`` tag can be used to maintain configuration of the
service.
