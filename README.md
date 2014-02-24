# Ansible role for ldap-account-manager

This is an incomplete role for ldap-account-manager free edition.

I tested it on CentOS 6.5

Example usage:

```
  vars:
    ldaps_port: 636
    ldap_dn: dc=example,dc=com
  roles:
    - role: ldap_account_manager
      lam_dn: "{{ ldap_dn }}"
      lam_admin: "cn=Manager,{{ ldap_dn }}"
      lam_ldaps_port: "{{ ldaps_port }}"
      lam_types: |
        activeTypes: user,group
        types: suffix_user: ou=people,{{ ldap_dn }}
        types: attr_user: #cn,#givenName,#sn,#mail
        types: modules_user: inetOrgPerson
        types: suffix_group: ou=groups,{{ ldap_dn }}
        types: attr_group: #cn,#description,#owner,#o,#member
        types: modules_group: groupOfNames
  tasks:
    - shell: lokkit -p {{ ldaps_port }}:tcp

```

