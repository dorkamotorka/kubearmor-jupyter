# Security Jupyter Notebooks using KubeArmor

```
helm upgrade --cleanup-on-fail --install my-jupyter jupyterhub/jupyterhub --namespace jupyter --create-namespace --values values.yaml
kubectl apply -f jupyter-policy.yaml
```

Default username and password for Jupyter Auth are both `ebpfchirp`.

- To `Block` by default:
```
kubectl annotate ns jupyter kubearmor-file-posture=block --overwrite
```
