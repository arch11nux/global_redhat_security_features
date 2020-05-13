Role Name: global_redhat_security_features

This role install and configure RHEL8 security. The role is composed from many subcategorys. By default all subcategorys are set to "no execute"

Requirements
------------

RHEL8

Role Variables
--------------

var_check_mode = False (roles/rglobal_redhat_security_features/defaults/main.yml)

Dependencies
------------

N/A

How is working:
===============
# Just check: 
  # SET the variable var_check_mode = True (roles/rglobal_redhat_security_features/defaults/main.yml)
  ansible-playbook checker.yml -i hosts --ask-become-pass  --tags "rglobal_redhat_security_features"
  - genarate a local report on each server (~rreport_global_redhat_security_features.out)

# check & apply *** D A N G E R ***: 
  # SET the variable var_check_mode = False (roles/rglobal_redhat_security_features/defaults/main.yml)
  ansible-playbook checker.yml -i hosts --ask-become-pass  --tags "rglobal_redhat_security_features"
  - genarate a local report on each server (~report_global_redhat_security_features.out)

NOTE:
=====
playbook exemple, when you call the role:

# Ansible Playbook - check Security Compliance on Linux servers 
- name: "Playing with Ansible"
  hosts: esxcentos7:esxcentos8:esxubuntu 
  user: <user_name> 
  sudo: yes 
  connection: ssh 
  gather_facts: true 
  vars: 
    var_global_redhat_security_features: True 
  tasks:
  - name: "global_redhat_security_features"
      # role rglobal_redhat_security_features: Security for RHEL8 | Linux RH8
    include_role:
      name: global_redhat_security_features
    tags:
      - RedHat8
      - global_redhat_security_features
    when: >
      var_global_redhat_security_features
      (ansible_facts['distribution'] == "RedHat" and ansible_facts['distribution_major_version'] == "8")

Structure:
==========
roles/global_redhat_security_features
  defaults/main.yml
  templates/report.j2
  tasks/main.yml
    tasks/fapolicyd.yml
    tasks/crypto-policies.yml
    tasks/redhatupdate.yml
    tasks/session-recording.yml

TAGS:
=====
- rglobal_redhat_security_features
- redhat8
# every task inside the role have it's own TAG
  - fapolicyd
  - crypto-policies
  - redhat_update
  - config_session-recording