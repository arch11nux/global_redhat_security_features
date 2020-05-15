Role Name: global_redhat_security_features

This role install and configure RHEL8 security. The role is composed from many subcategorys. By default all subcategorys are set to "no execute"

Requirements
------------

RHEL8

Role Variables
--------------

var_check_mode = False (roles/global_redhat_security_features/defaults/main.yml)

Dependencies
------------

N/A

How is working:
===============
# Just check: 
  # SET the variable var_check_mode = True (roles/rglobal_redhat_security_features/defaults/main.yml)
  ansible-playbook checker.yml -i hosts --ask-become-pass  --tags "global_redhat_security_features"
  - genarate a local report on each server (~global_redhat_security_features_report.out)

# check & apply *** D A N G E R ***: 
  # SET the variable var_check_mode = False (roles/rglobal_redhat_security_features/defaults/main.yml)
  ansible-playbook checker.yml -i hosts --ask-become-pass  --tags "global_redhat_security_features"
  - genarate a local report on each server (~global_redhat_security_features_report.out)


Structure:
==========
roles/global_redhat_security_features
  defaults/main.yml
  templates/global_redhat_security_features_report.j2
  tasks/main.yml
    tasks/redhat_update.yml
    tasks/redhat6_setup.yml
    tasks/redhat7_setup.yml
    tasks/redhat8_setup.yml
      tasks/redhat8_fapolicyd.yml
      tasks/redhat8_crypto-policies.yml
      tasks/redhat8_session-recording.yml

TAGS:
=====
- global_redhat_security_features
- redhat8
# every task inside the role have it's own TAG
  - redhat_update
  - redhat8_fapolicyd
  - redhat8_crypto_policies
  - redhat8_config_session-recording