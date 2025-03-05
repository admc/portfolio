---
runme:
  id: 01HWZZN2JPA96VBHV23PC6C1CC
  version: v3
---

# Ops Workflow for k8s/emojivoto

## Prerequisites

Install AWS CLI via Homebrew on macOS

```sh {"id":"01J9W2PAD43AG65VQBME3TFAB4"}
brew install awscli
aws --version
```

Configure it with the values from, e.g. `adam (AWS Stateful IAM)` in 1password.

```sh {"id":"01J9W2Q0KYHTZP84JKAQXV4FZG"}
aws configure
```

## Check setup

```sh {"id":"01J9W29GXPMRWEA3EBH3CDH4FG","promptEnv":"no","terminalRows":"3"}
export AWS_PROFILE="default"
export AWS_REGION="us-east-2"
export EKS_CLUSTER_NAME="demo-1"

echo "Using AWS_PROFILE=${AWS_PROFILE} in AWS_REGION=${AWS_REGION} with EKS_CLUSTER_NAME=${EKS_CLUSTER_NAME}."
```

```sh {"id":"01J9W28QQ0CR66W9G21SGECCBH","interactive":"true","terminalRows":"10"}
aws sts get-caller-identity
```

```sh {"id":"01J9W2B1RXVJTRHWF181MQSNFP"}
https://us-east-2.console.aws.amazon.com/eks/home?region=${AWS_REGION}#/clusters
```

```sh {"id":"01J9W35N9ZR3VGJRGKEKMMMZZ6"}
aws eks update-kubeconfig --region $AWS_REGION --name $EKS_CLUSTER_NAME --profile $AWS_PROFILE
```

```sh {"id":"01JATS3JSX8DABG4783GRCHYQ8"}
kubectl config current-context
```

```sh {"id":"01JATS4WDGC5F26XMB07696RNX"}
kubectl config use-context arn:aws:eks:us-east-2:381491863923:cluster/demo-1

```

```sh {"id":"01J9W3DCPJ902G7E5RNFPXJ19W","terminalRows":"20"}
kubectl get pods -A
```

If you are running this demo locally, please proceed to [setup.md](setup.md).
