.. Copyright (C) 2020 Wazuh, Inc.

.. _wazuh_agent_package_fedora22_or_greater:

Fedora from package
===================

The RPM package is suitable for installation on Fedora 22 or greater. For other operating systems or Linux distributions, please check the list: :ref:`Install Wazuh agent <installation_agents>`.

.. note:: All the commands described below need to be executed with root user privileges.

Installing Wazuh agent
----------------------

1. Adding the Wazuh repository:

  .. code-block:: console

    # rpm --import http://packages.wazuh.com/key/GPG-KEY-WAZUH
    # cat > /etc/yum.repos.d/wazuh.repo <<\EOF
    [wazuh_repo]
    gpgcheck=1
    gpgkey=https://packages.wazuh.com/key/GPG-KEY-WAZUH
    enabled=1
    name=Wazuh repository
    baseurl=https://packages.wazuh.com/3.x/yum/
    protect=1
    EOF

2. On your terminal, install the Wazuh agent. You can choose installation or deployment:

  a) Installation:

    .. code-block:: console

      # dnf install wazuh-agent

    Now that the agent is installed, the next step is to register and configure it to communicate with the manager. For more information about this process, please visit the document:  :ref:`user manual<register_agents>`.

  b) Deployment:

    You can automate the agent registration and configuration using variables. It is necessary to define at least the variable ``WAZUH_MANAGER``. The agent will use this value to register and it will be the assigned manager for forwarding events.

    .. code-block:: console

      # WAZUH_MANAGER="10.0.0.2" dnf install wazuh-agent

    See the following document for additional deployment options: :ref:`deployment variables <deployment_variables_dnf>`.

3. **(Optional)** Disable the Wazuh repository:

  We recommend maintaining the Wazuh manager version greater or equal to that of the Wazuh agents. As a result, we recommended disabling the Wazuh repository in order to prevent accidental upgrades. To do this, use the following command:

  .. code-block:: console

    # sed -i "s/^enabled=1/enabled=0/" /etc/yum.repos.d/wazuh.repo

Alternatively, if you want to download the wazuh-agent package directly, or check the compatible versions, you can do it from :ref:`here <packages>`.

Uninstall
---------

To uninstall the agent:

    .. code-block:: console

      # dnf remove wazuh-agent

There are files marked as configuration files. Due to this designation, the package manager doesn't remove those files from the filesystem. The complete files removal action is a user responsibility. It can be done by removing the folder ``/var/ossec``.