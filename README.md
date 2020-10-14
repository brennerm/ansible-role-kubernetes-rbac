ansible-role-kubernetes-rbac
=========

This role allows you to create Role, ClusterRole, RoleBinding and ClusterRoleBinding Kubernetes resources.

Requirements
------------

This role uses the community.kubernetes.k8s module which needs some [requirements](https://docs.ansible.com/ansible/latest/collections/community/kubernetes/k8s_module.html#requirements).

Role Variables
--------------

- k8s_roles: A list of parameters for [Role](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-and-clusterrole) resources that will be created
- k8s_clusterroles: A list of parameters for [ClusterRole](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-and-clusterrole) resources that will be created
- k8s_rolebindings: A list of parameters for [RoleBinding](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#rolebinding-and-clusterrolebinding) resources that will be created
- k8s_clusterrolebindings: A list of parameters for [ClusterRoleBinding](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#rolebinding-and-clusterrolebinding) resources that will be created

Check the [defaults/main.yml](defaults/main.yml) for some examples.

Switching between Kubernetes cluster
------------------------------------

Read through the [community.kubernetes.k8s module documentation](https://docs.ansible.com/ansible/latest/collections/community/kubernetes/k8s_module.html) to understand how to set the Kubernetes cluster to work on.

Example Playbook
----------------

```yaml
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
```

License
-------

MIT

Author Information
------------------

Max Brenner <xamrennerb@gmail.com>
