fortress-in-a-box
=================

Provides an Ansible playbook that installs Fortress on Redhat-based Linux systems. The ansible scripts are based on the ten minute guide (https://directory.apache.org/fortress/gen-docs/latest/apidocs/org/apache/directory/fortress/core/doc-files/ten-minute-guide.html).

Configuration

- For openldap, need to download an rpm (https://symas.com/downloads/) and place in roles/openldap/files. Also make sure name of file matches in roles/openldap/tasks/main.yml.
- Can be configured to run with either apacheds or openldap. Modify fortress-in-a-box.yml and enable either apacheds or openldap
- Currently configured to build fortress from the latest source, this can be overridden with the {{fortress_git_version}} variable
- Need to add vagrant box (vagrant box add http://developer.nrel.gov/downloads/vagrant-boxes/CentOS-6.4-i386-v20130427.box). Can use other boxes, just make the Vagrantfile is modified correctly.

General Notes

- The firewall on the VM is turned off and disabled by default
- Default logon for commander ui is test/password

Apache DS Notes

- If the doesn't shut down cleanly, the pid file for ApacheDS won't get propertly removed. This will cause it to appear like the AapcheDS service is running. To resolve this issue, remove the pid file in /var/lib/apacheds...), then start the service service apacheds... start

- The Fortress Commander UI won't start properly if ApacheDS isn't running. When starting the VM, tomcat will start before ApacheDS, so you will have to go into the tomcat admin manager application and manually start fortress-web.

Tomcat Notes

- Manager GUI admin login is admin/password
- The tomcat role was copied and modified from here (https://github.com/ansible/ansible-examples/tree/master/tomcat-standalone)
