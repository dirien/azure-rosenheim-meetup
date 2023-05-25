# Azure Rosenheim Meetup

This repository contains the demo code for the Azure Rosenheim Meetup.
See https://www.meetup.com/azure-meetup-rosenheim/events/292822487/ for more details.

## Infrastructure Deployment

The infrastructure deployment will be done using Pulumi Azure Native. As language, we will use Go.

```bash
cd infrastructure-go

pulumi preview
pulumi up
```

After the infrastructure is deployed, we need to get the kubeconfig from the stack output and save it to a file.

```bash
pulumi stack output kubeconfig --show-secrets > rosenheim.yaml
```

This is not a necessary step as we're going to use Pulumi Stack References to get the kubeconfig from the infrastructure
stack. See https://www.pulumi.com/learn/building-with-pulumi/stack-references/ for more details.

## Application Deployment

This deployment will be done using Pulumi AI. Head over to https://pulumi.com/ai and enter following prompt:

```text
Imagine you are a Kubernetes application developer and need to use a stack reference (dirien/infrastructure-go/dev) to
get Kubeconfig from a different stack.
Then you create a Nginx (use the latest tag for the image) deployment with a custom config map, which contains "Hello
Azure Rosenheim Meetup" as part
of the nginx.conf. This config map should then be mounted on /etc/nginx/. Finally, expose this deployment via a service
of type Loadbalancer.

Create only one Kubernetes provider and pass it as dependency to the resources.

Finally Export the address of the loadbalancer as output by interpolating the `http` protocol to it.
```


```bash
cd application-ts
pulumi preview
```
