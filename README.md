# Kube Namespace
Run multiple kubectl commands in the same namespace.

# Table Of Contents
- [Overview](#overview)
- [Tutorial](#tutorial)
- [Install](#install)
- [How It Works](#how-it-works)

# Overview
Kube Namespace makes it easier to run multiple `kubectl` commands in the same
namespace.  

Without Kube Namespace the `--namespace` argument would have to be given every `kubectl` command:

```
kubectl --namespace product-foo-api get all
kubectl --namespace product-foo-api describe pod/api-server-0
kubectl --namespace product-foo-api exec api-server-0 /bin/bazz
```

With Kube Namespace running multiple commands in the same namespace is much simplier:

```
kubens use product-foo-api

kubectl get all
kubectl describe pod/api-server-0
kubectl exec api-server-0 /bin/bazz
```

# Tutorial
First set which namespace you would like to work in:

```
kubens use <namespace>
```

Then run `kubectl` commands as you normally would:

```
kubectl get services
kubectl describe services/api-server
```

If you need to override the namespace for one command the `kubectl --namespace` 
argument can be used as normal:

```
kubectl --namespace foo-bar get all
```

To see what namespace you are working in:

```
kubens show
```

To stop working in a specific namespace:

```
kubens exit
```

# Install
Complete the following steps to install Kube Namespace:

1. Clone down the Kube Namespace repo
   ```
   git clone git@github.com:Noah-Huppert:kube-namespace.git <install directory>
   ```
2. Source the `kubens` file in the Kube Namespace repository
   ```
   # In your shell profile
   . <install directory>/kubens
   ```
3. Make an alias to the Kube Namespace command
   ```
   # In your shell profile
   alias kubectl="kubens run"
   ```
   This allows you to use the `kubectl` with enhanced namespace functionality

# How It Works
Kube Namespace provides a simple `kubens` bash function.  

This function has 4 sub-commands:

- `use NAMESPACE`
	- Records which Kubernetes namespace the user wants to work in by 
	  setting the `KUBENS_NAMESPACE` environment variable
- `show`
	- Shows which Kubernetes namespace a user is working in by printing the 
	  `KUBENS_NAMESPACE` environment variable
- `exit`
	- Clears the desired Kubernetes namespace by unsetting the 
	  `KUBENS_NAMESPACE` environment variable
- `run ARGS...`
	- Executes the normal `kubectl` binary with the `--namespace` argument 
	  set to the value of the `KUBENS_NAMESPACE` environment variable
	- If the user provides their own `--namespace` argument value it will 
	  override the namespace set by the Kube Namespace tool
