# Kube Namespace
Run all kubectl commands in the same namespace.

# Table Of Contents
- [Overview](#overview)
- [Install](#install)
- [How It Works](#how-it-works)

# Overview
Kube Namespace makes it easier to run multiple commands in the same namespace.  

Simply indicate which namespace you would like to work in:

```
kubens use <namespace>
```

Then run `kubectl` commands as you normally would:

```
kubectl get all
```

If you need to override the namespace for one command the `kubectl --namespace` 
argument can be used as normal:

```
kubectl --namespace foo-bar get all
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
2. Add the Kube Namespace repository to your path
   ```
   # In your shell profile
   export PATH="$PATH:<install directory>
   ```
3. Make an alias to the Kube Namespace command
   ```
   # In your shell profile
   alias kubectl="kubens run"
   ```
   This allows you to use the `kubectl` with enhanced namespace functionality

# How It Works
Kube Namespace provides a single `kubens` bash script.  

This bash script has 3 sub-commands:

- `use NAMESPACE`
	- Records which Kubernetes namespace the user wants to work in by 
	  settings the `KUBENS_NAMESPACE` environment variable
- `exit`
	- Clears the desired Kubernetes namespace by upsetting the 
	  `KUBENS_NAMESPACE` environment variable
- `run ARGS...`
	- Executes the normal `kubectl` binary with the `--namespace` argument 
	  set to the value of the `KUBENS_NAMESPACE` environment variable
	- If the user provides their own `--namespace` argument value it will 
	  override the namespace set by the Kube Namespace tool
