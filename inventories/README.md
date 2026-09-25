# Inventories

Lab inventory examples belong here. Do not commit credentials, tokens, private keys, vault passwords, or environment secrets.

For Tomcat testing, copy `lab/hosts.example.yml` to `lab/hosts.yml`, edit the target host, and copy only required variables from `lab/group_vars/tomcat.example.yml` into `lab/group_vars/tomcat.yml`.

The repository-root `ansible.cfg` automatically supplies the lab inventory and role search paths, so tester commands can be run from the repository root.
