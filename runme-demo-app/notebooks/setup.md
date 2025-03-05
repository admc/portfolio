---
cwd: ..
runme:
  id: 01HR5S2KC0Y8MPR9XDAH7N8BDG
  version: v3
---

# Application Setup

This guide is designed to walk you through the basics of the use case.

Validate your Kubernetes setup by running:

```bash {"id":"01HR53VC0NT8SQZD6HXGDKA3PP","name":"kubectl-version"}
kubectl version
```

```bash {"id":"01JATS5SDX6VPFR21VTGT3H5P2"}
$ kubectl config current-context
```

```bash {"id":"01JATS8B499W969ZEEBYFW2XRA"}
$ kubectl get pods
```

You should see output with both a `Client Version` and `Server Version`
component.

## Install Emojivoto

Let's install a demo application called _Emojivoto_. Emojivoto is a simple
standalone Kubernetes application that uses a mix of gRPC and HTTP calls to
allow the user to vote on their favorite emojis.

Tail the pods

```bash {"id":"01HRT5035FNSDAVBVJAYMKJZ90","name":"tail-pods"}
kubectl get pods -n emojivoto -w
```

Install Emojivoto into the `emojivoto` namespace by running:

```bash {"id":"01HR53VC0NT8SQZD6HXSZFDSA4","name":"install-emojivoto"}
kubectl apply -f emojivoto.yaml
```

Forward the port to use the web app locally

```bash {"background":"true","id":"01HR53VC0NT8SQZD6HXWJ2K9EW","name":"forward-web-svc"}
kubectl -n emojivoto port-forward svc/web-svc 8080:80
```

Now visit [http://localhost:8080](http://localhost:8080). Voila! You should see
Emojivoto in all its glory.

## Next up

Proceed with [troubleshoot.md](troubleshoot.md).
