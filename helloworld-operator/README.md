# Bootstrap
Used these values to setup this with operator-sdk cli:
```bash
#PWD = this folder!
operator-sdk init --domain maik.fi --repo github.com/maikdotfi/k8s-operator/helloworld-operator
# API group will be maik?
operator-sdk create api --group maik --version v1alpha1 --kind Helloworld --resource --controller
```

