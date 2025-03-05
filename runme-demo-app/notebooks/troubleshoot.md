---
cwd: ../
runme:
  id: 01HR5RX1R59TDJYSSZ047ASRYN
  version: v3
---

## Troubleshooting / Health Checks

Once Emojivoto is deployed to kubernetes (k8s), it's important to know that all
the different pieces of the infrastructure and the application are working as
expected. To do this we interact with each of the service endpoints work
individually, the output here is very useful for troubleshooting.

Using the `run all` button is a good way to asynchronously run all each cell,
which function as health checks.

### Web

These are the Health checks that ensure the web application is available, on the
desired port and subsequent services respond as expected.

```sh {"id":"01HR5T19JXBE5V16A8F4R5H33R","interpreter":"","name":"curl-webapp"}
curl --fail -I http://localhost:8080/
```

Tail the logs so we can see in real-time what's going on in the cluster with the
app

```sh {"background":"true","id":"01HR5T425DSYRGSV8D3EGQGJZ2","name":"tail-web-logs"}
kubectl logs -f -n emojivoto -l app=web-svc -c web-svc
```

A simple health check to test that the vote endpoint for sunglasses is passing.

```sh {"id":"01HR5T21PCHPNQPHW6GDVZS814","name":"web-vote-sunglasses"}
curl --fail -I "http://localhost:8080/api/vote?choice=:sunglasses:"
```

Test the vote doghnut endpoint

```sh {"id":"01HR5T60PHB4V6ABF2PTFFAN56","name":"web-vote-doughnut"}
curl --fail "http://localhost:8080/api/vote?choice=:doughnut:"
```

### Voting (use kubectl to connect to and log the voting service)

Setup the port forwarding so kubectl can talk to the voting-svc on a local port

```sh {"background":"true","id":"01HR5RYSG37A85T3ZX5EW14PDS","name":"forward-voting-svc"}
kubectl -n emojivoto port-forward svc/voting-svc 8082:8080
```

Log the voting service

```sh {"background":"true","id":"01HR5SH5DKNGD4T6JTVJVMRAC5","name":"tail-voting-logs"}
kubectl logs -f -n emojivoto -l app=voting-svc -c voting-svc
```

Register a vote via GRPC:

```sh {"id":"01HR5S705QYYA7D722QJNR8BCE"}
grpcurl -plaintext -proto protos/Voting.proto \
    -d '' \
    localhost:8082 emojivoto.v1.VotingService.VoteHeartEyesCat
```

Get an error for the doughnut:

```sh {"id":"01HR5T9P437CTT7ERT9XDQ60KY"}
grpcurl -plaintext -proto protos/Voting.proto \
    -d '' \
    localhost:8082 emojivoto.v1.VotingService.VoteDoughnut
```

At this point, you should have a pretty good understanding of the state of the
cluster and app.

## Next Step

Final step is [teardown.md](teardown.md).
