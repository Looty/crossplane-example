# Commands

`kind create cluster --config=cluster-config.yml`

`helm repo add crossplane-stable https://charts.crossplane.io/stable`

`help repo update`

`helm install crossplane --namespace crossplane-system --create-namespace crossplane-stable/crossplane`

> for metrics in kind cluster<br>
`helm upgrade --install --set args={--kubelet-insecure-tls} metrics-server metrics-server/metrics-server --namespace kube-system`

# NOTES!
1. You must have a secret named `aws-secret-creds` in namespace `crossplane-system` with a data of `creds` with your AWS creds
2. Populate your public IP in `aws/ec2-example/resources/securitygroup.yaml` at `spec.forProvider.ingress[*].ipRanges["cidrIp"]` 

# References:
https://crossplane.io/docs/v1.9/getting-started/install-configure.html
https://github.com/crossplane-contrib/provider-aws/tree/master/examples/ec2


### Creating the secret locally
`AWS_PROFILE=default && echo -e "[default]\naws_access_key_id = $(aws configure get aws_access_key_id --profile $AWS_PROFILE)\naws_secret_access_key = $(aws configure get aws_secret_access_key --profile $AWS_PROFILE)" > creds.conf`

`kubectl create secret generic aws-secret-creds -n crossplane-system --from-file=creds=./creds.conf`