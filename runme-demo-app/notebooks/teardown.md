---
cwd: ..
runme:
  id: 01HR5S3M26C8TVPR7JDJEHSF34
  version: v3
---

## Teardown

Get back into the original state, a good idea for cloud cost savings.

Free the forwarded port

```bash {"id":"01HRT3VTYZ3NYXK51A7M3VEJP2","name":"free-ports"}
lsof -ti:8080 | xargs kill -9 || true 
```

Make sure the right cluster is selected

```bash {"id":"01JATS6PXYNY73ZY1CT9ZDM4YV"}
$ kubectl config current-context
```

```bash {"id":"01HRAG9Z8Y8J1NASYCE0JYJ4M7","name":"check-selected-cluster"}
kubectl config get-contexts

```

```bash {"background":"true","id":"01HR5TEYQK0K2BF014JQB06V0A","name":"watch-emojivoto-ns","terminalRows":"18"}
kubectl get pods -n emojivoto -w
```

```bash {"id":"01HR5RE9G8DG33NW4SSVXPHWN3","interactive":"false","name":"uninstall-emojivoto"}
kubectl delete -f emojivoto.yaml
```

## That's it! 👏
