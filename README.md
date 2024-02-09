# Random Secret Generator
This YAML template will apply a generator that will create random values for secrets and update them via the API, this image is based off `bitnami/kubectl:latest`

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
# Apply all resources
kubectl apply -f $(pwd)/random-secret-generator/lib/

# --------------------------
# Use your shell to generate the template and deploy it manually
rm -r $(pwd)/random-secret-generator/Deployment.yaml 2>/dev/null; \
    for i in $(find $(pwd)/random-secret-generator/lib/ -type f); do \
    kv=$(cat $i && echo -e "\n---"); echo $kv >> $(pwd)/random-secret-generator/Deployment.yaml; \
    done

# Deploy the freshly generated YAML
kubectl apply -f Deployment.yaml
```


--- 

## Generating a password for your Secret with `base64` encoding

```bash
# Generate random 32 length password from kernel
    $ head /dev/urandom | tr -dc A-Za-z0-9 | head -c 32 | base64
    # Output: 'U1MwNkQ4ZXFHNm51UlBYR0lrZ01uTjUzZm1KamUxdmw='

# Generate from Base64
    $ echo -n "mytestingpassword" | base64
    # Output: 'bXl0ZXN0aW5ncGFzc3dvcmQ='

# Generate and store into a variable
    $ MY_PASS=$(echo -n "mytestingpassword" | base64)
    $ echo "My Password is: '$MY_PASS'"
```

## Decoding your password

```bash
$ echo "bXl0ZXN0aW5ncGFzc3dvcmQ=" | base64 -d
# Output: 'mytestingpassword'
```
