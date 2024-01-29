# Random Secret Generator
This YAML template will apply a generator that will create random values for secrets and update them via the API

`Secret` resources can be directly mounted to other containers if made to multiple, `Kind: Opaque` is a `K:V` env variable that cannot be mutated but updated on a `CronJob`. 

This means that we can mount our secret to a sidecar container or a primary container and read them directly from our non-tty shell environment.

# Installation
Clone the repo and apply the Kubernetes resources to your cluster.
```bash
git clone https://github.com/txj-xyz/random-secret-generator
```

# Usage
Install YAML from kubectl access.
```bash
kubectl apply -f $(pwd)/random-secret-generator/lib/
```
