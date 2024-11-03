# Security Jupyter Notebooks using KubeArmor

The Jupyter Notebook is a web-based interactive computing platform, for interactively developing and visualizing AI and data science projects. 

But, at the same time it provides elevated privileges to execute arbitrary code, which makes it vulnerable to malicious code execution in case attacker gains access.

This repository showcases, how you can configure runtime security using KubeArmor to prevent such situations.

## How to try it yourself

Jupyter Hub can be installed using:
```
helm upgrade --cleanup-on-fail --install my-jupyter jupyterhub/jupyterhub --namespace jupyter --create-namespace --values values.yaml
```

Default username and password for Jupyter Auth are both `ebpfchirp`.

Since this is a public repo, please update the username and password in case you plan to run it on a public IP. 

You can uninstall the helm chart afterwards using:
```
helm uninstall my-jupyter --namespace jupyter
```

To enforce the runtime security first [install KubeArmor](https://docs.kubearmor.io/kubearmor/quick-links/deployment_guide) and then apply the security policy:
```
kubectl apply -f jupyter-policy.yaml
```

KubeArmor by default only audits the events. If you want to block everything and just allow the actions as specified in the policy above, you need to execute:

```
kubectl annotate ns jupyter kubearmor-file-posture=block --overwrite
```

To try it out, run the `exploit.ipynb` script. You should get a `Permissions denied` error.
