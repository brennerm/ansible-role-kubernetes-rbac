ansible-role-kubernetes-rbac
=========

This role allows you to create Role, ClusterRole, RoleBinding and ClusterRoleBinding Kubernetes resources.

Requirements
------------

This role uses the community.kubernetes.k8s module which needs some [requirements](https://docs.ansible.com/ansible/latest/collections/community/kubernetes/k8s_module.html#requirements).

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Switching between Kubernetes cluster
------------------------------------

Read through the [community.kubernetes.k8s module documentation](https://docs.ansible.com/ansible/latest/collections/community/kubernetes/k8s_module.html) to understand how to set the Kubernetes cluster to work on.

Example Playbook
----------------

- hosts: localhost
  roles:
  - role: ansible-role-kubernetes-rbac
    k8s_roles:
    - name: pod-reader
      namespace: default
      rules:
      - resources: ["pods"]
          verbs: ["get", "watch", "list"]
    k8s_rolebindings:
    - name: read-pods
      namespace: default
      users:
      - name: jane
      groups:
      - name: pod-readers
      role: pod-reader

License
-------

MIT

Author Information
------------------

Max Brenner <xamrennerb@gmail.com>
