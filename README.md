# Kustomize illustrated

Its much easier to understand how [kustomize](https://github.com/kubernetes-sigs/kustomize) works if you see some pictures ...

## Base

The gist of kustomize is in the structure:
- just put plane old yaml files (deployment/svc) into a directory
- add an extra `kustomization.yaml` file:

![base](img/base.png)

Done, that was it, now you know kustomize ... (hint: there is more)

You can use `kubectl apply` but instead of `-f` use `-k`:
```
kubectl apply -k base
```

## Prod/QA separated namespaces

Now imagine you want to use the same 2 resources for qa and prod.
Easy, you create 2 new directories, each with its own kustomization.yaml:

```
├── base
│   ├── kustomization.yaml
│   ├── deploy.yaml
│   └── svc.yaml
├── prod
│   └── kustomization.yaml
└── qa
    └── kustomization.yaml
```

Both new kustomization.yaml will reference to the `base` directory, and to avoid any
collision, they define they own namespace:

![base](img/kustomize-ns.png)

The easiest way is just to simply add a `namespace` property to 
