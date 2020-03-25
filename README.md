Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.




Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
    ---
    - hosts:  all
      become: yes
      become_method: sudo
      gather_facts: false
      ignore_errors: true
      ignore_unreachable: true
      vars:
       ignore_errors: true
       ignore_unreachable: true
      tasks:
       - name: "Check if the host is reachable"
         setup:
          register: setup_status
          ignore_errors: yes
         tags:
          - always

       - name: "Group reachable hosts"
         group_by: key=reachable
         ignore_errors: yes
         when:
          - setup_status is defined and not setup_status.unreachable is defined
        tags:
         - always

    - hosts: reachable
      become: yes
      become_method: sudo
      gather_facts: true
      ignore_errors: false
      ignore_unreachable: true
      vars:
       ignore_errors: false
       ignore_unreachable: true
       rhel7cis_level1: true
       rhel7cis_level2: true
       rhel7cis_tmp_ensure_all: true
       rhel7cis_time_synchronization: chrony
       rhel7cis_enable_auditd: true
       rhel7cis_permit_ssh_root_login_disabled: false
       rhel7cis_modify_dot_forward_files: true
       rhel7cis_modify_dot_netrc_files: true
       rhel7cis_modify_dot_netrc_files_group: true
       rhel7cis_modify_dot_rhosts_files: true

      roles:
       - role: RHELHardening
      post_tasks:
       - meta: clear_host_errors
         when: ignore_unreachable

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
