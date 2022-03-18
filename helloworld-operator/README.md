# Helloworld operator
This is just a simple operator to get started with Operator SDK based on the [tutorial](https://sdk.operatorframework.io/docs/building-operators/golang/tutorial/), but I wanted to change the naming so I can't just copy-paste.
## Bootstrap
Used these values to setup this with operator-sdk cli:
```bash
#PWD = this folder!
operator-sdk init --domain maik.fi --repo github.com/maikdotfi/k8s-operator/helloworld-operator
# API group will be maik?
operator-sdk create api --group maik --version v1alpha1 --kind Helloworld --resource --controller
```
> Note this means the resource apiVersion will be maik.maik.fi/v1alpha1 and kind Helloworld, which is a stupid apiVersion and I should have used another group name

# Local development
Operators can be developed locally using kind and local registry (running in docker container):
```bash
cd kind
sh start.sh
```
> **Note:** tested on kind 0.11.1

## Tests and image build
When you run docker build/push some tests will also be run, make sure these run in a k3d cluster instead of local (unless you have etcd installed locally etc.):
```bash
export USE_EXISTING_CLUSTER=true
make docker-build docker-push
```

## Deploy
Deploying to cluster is really simple:
```bash
make deploy
```
### Deploying CRD
There's an example CRD in the kind folder:
```bash
kubectl apply -f helloworld-crd.yaml
```

## k8s CRD confusion
The naming of this example didn't really please me, I couldn't even figure out how to launch the CRD firstly. Here's how to find out:

```bash
kubectl get crds
kubectl explain <name-of-crd>
```

The crd name looked funky but explain gives sane looking stuff still.
