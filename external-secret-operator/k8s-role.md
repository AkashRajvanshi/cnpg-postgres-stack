## Add k8s access openbao

```bash
# Kubernetes Policies For kubernets
bao auth enable kubernetes

apiVersion: v1
kind: ServiceAccount
metadata:
  name: bao-sa
  namespace: openbao
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: bao-auth-delegator
subjects:
- kind: ServiceAccount
  name: bao-sa
  namespace: openbao
roleRef:
  kind: ClusterRole
  name: system:auth-delegator
  apiGroup: rbac.authorization.k8s.io


export OPEN_BAO_SA_NAME="bao-sa"
export OPEN_BAO_NAMESPACE="openbao"

export KUBE_HOST_IP=$(kubectl get svc kubernetes -n default -o jsonpath='{.spec.clusterIP}')
export KUBE_HOST="https://$KUBE_HOST_IP:443"


export SA_TOKEN=$(kubectl create token ${OPEN_BAO_SA_NAME} --namespace ${OPEN_BAO_NAMESPACE})
export KUBE_CERT=$(kubectl get configmap kube-root-ca.crt -n default -o jsonpath='{.data.ca\.crt}')


bao write auth/kubernetes/config \
    kubernetes_host="${KUBE_HOST}" \
    token_reviewer_jwt="${SA_TOKEN}" \
    kubernetes_ca_cert="${KUBE_CERT}"

bao policy write read-all-secrets - <<EOF
path "secrets/*" {
  capabilities = ["read", "list"]
}
EOF

bao write auth/kubernetes/role/openbao-readonly \
    bound_service_account_names="*" \
    bound_service_account_namespaces="postgres" \
    policies="read-all-secrets" \
    ttl="20m"


bao read auth/kubernetes/config
bao read auth/kubernetes/role/openbao-readonly

Key                                         Value
---                                         -----
alias_name_source                           serviceaccount_uid
bound_service_account_names                 [*]
bound_service_account_namespace_selector    n/a
bound_service_account_namespaces            [openbao]
policies                                    [read-all-secrets]
token_bound_cidrs                           []
token_explicit_max_ttl                      0s
token_max_ttl                               0s
token_no_default_policy                     false
token_num_uses                              0
token_period                                0s
token_policies                              [read-all-secrets]
token_strictly_bind_ip                      false
token_ttl                                   20m
token_type                                  default

```
