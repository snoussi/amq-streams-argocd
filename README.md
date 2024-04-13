# Install OpenShift GitOps operator
- Use the Openshift console or use this command line

```
$ oc apply -k https://github.com/redhat-cop/gitops-catalog/openshift-gitops-operator/operator/overlays/latest
```

- Give cluster-admin privileges to ArgoCD

```
oc adm policy add-cluster-role-to-user cluster-admin -z openshift-gitops-argocd-application-controller -n openshift-gitops
```

- Get the ArgoCD admin password

```
argocdPass=$(oc get secret/openshift-gitops-cluster -n openshift-gitops -o jsonpath='{.data.admin\.password}' | base64 -d) && echo $argocdPass
```

- Login to ArgoCD with `admin` and the value of `$argocdPass`


# Demo

```
oc apply -f apps/amq-streams-application-set.yml 
```

```
oc delete -f apps/amq-streams-application-set.yml 
```