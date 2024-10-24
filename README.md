# Security Jupyter Notebooks using KubeArmor

```
helm upgrade --cleanup-on-fail --install my-jupyter jupyterhub/jupyterhub --namespace jupyter --create-namespace --values values.yaml
kubectl apply -f jupyter-policy.yaml
```

Default username and password for Jupyter Auth are both `ebpfchirp`.

Since this is a public repo, please update the username and password in case you plan to run it on a public IP. 

You can uninstall the helm chart afterwards using:
```
helm uninstall my-jupyter --namespace jupyter
```

- To `Block` by default:
```
kubectl annotate ns jupyter kubearmor-file-posture=block --overwrite
```
