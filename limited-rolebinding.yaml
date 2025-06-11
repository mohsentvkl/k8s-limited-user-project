apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: limited-rolebinding
  namespace: limited-ns
subjects:
- kind: ServiceAccount
  name: limited-user
  namespace: limited-ns
roleRef:
  kind: Role
  name: limited-role
  apiGroup: rbac.authorization.k8s.io
