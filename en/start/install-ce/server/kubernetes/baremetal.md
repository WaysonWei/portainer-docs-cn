# Install Portainer CE on your Kubernetes environment


These installation instructions are for Portainer Community Edition (CE). For Portainer Business Edition (BE) refer to the [BE install documentation](../../../install/server/kubernetes/baremetal.md).


## Introduction

Portainer consists of two elements, the _Portainer Server_ and the _Portainer Agent_. Both elements run as lightweight containers on Kubernetes.

To get started, you will need:

* A working and up to date Kubernetes cluster.
* Access to run `helm` or `kubectl` commands on your cluster.
* Cluster Admin rights on your Kubernetes cluster. This is so Portainer can create the necessary `ServiceAccount` and `ClusterRoleBinding` for it to access the Kubernetes cluster.
* A `default` StorageClass configured (see below).

The installation instructions also make the following assumptions about your environment:

* Your environment meets [our requirements](../../../requirements-and-prerequisites.md). While Portainer may work with other configurations, it may require configuration changes or have limited functionality.
* Kubernetes RBAC is enabled and working (this is required for the access control functionality in Portainer).
* You will be using the `portainer` namespace for Portainer. At present this is a requirement - other namespaces are currently unsupported.
* Kubernetes' metrics server is installed and working (if you wish to use the metrics within Portainer).

## Data Persistence

Portainer requires data persistence, and as a result needs at least one StorageClass available to use. Portainer will attempt to use the default StorageClass during deployment. If you do not have a StorageClass tagged as `default` the deployment will likely fail.


We recommend using block storage for Kubernetes rather than network storage for the best performance and reliability, but do pay attention to the IOPS of your block storage devices when choosing the volume to use as some options are slower than others.


You can check if you have a default StorageClass by running the following command on your cluster:

```
kubectl get sc
```

and looking for a StorageClass with `(default)` after its name:

```
root@kubemaster01:~# kubectl get sc
NAME                            PROVISIONER                                   RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
managed-nfs-storage (default)   k8s-sigs.io/nfs-subdir-external-provisioner   Delete          Immediate           false                  11d
```

To set a StorageClass as default, you can use the following:

```
kubectl patch storageclass <storage-class-name> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```

replacing `<storage-class-name>` with the name of your StorageClass. Alternatively, if you are installing using our Helm chart, you can pass the following parameter in your helm install command to specify the StorageClass to use for Portainer:

```
--set persistence.storageClass=<storage-class-name>
```


In some Kubernetes clusters (for example microk8s), the default StorageClass simply creates hostPath volumes, which are not explicitly tied to a particular node. In a multi-node cluster, this can create an issue when the pod is terminated and rescheduled on a different node, "leaving" all the persistent data behind and starting the pod with an "empty" volume.

While this behavior is inherently a limitation of using hostPath volumes, a suitable workaround is to use add a nodeSelector to the deployment, which effectively "pins" the Portainer pod to a particular node. You can do this by editing your own values.yaml file to set the nodeSelector value:

`nodeSelector: kubernetes.io/hostname: \<YOUR_NODE_NAME>`

or alternatively follow the instructions below for each deployment method.


## Deployment

To deploy Portainer within a Kubernetes cluster you can use our provided Helm charts or YAML manifests.

### Deploy using Helm


Ensure you're using at least Helm v3.2, which includes support for the `--create-namespace` argument.


First add the Portainer Helm repository by running the following commands:

```
helm repo add portainer https://portainer.github.io/k8s/
helm repo update
```

Once the update completes, you're ready to begin the installation. Which method you choose will depend on how you wish to expose the Portainer service:



Using the following command, Portainer will be available on port `30779` for HTTPS:

```
helm upgrade --install --create-namespace -n portainer portainer portainer/portainer \
    --set tls.force=true \
    --set image.tag=lts
```


By default, Portainer generates and uses a self-signed SSL certificate to secure port `30779`. Alternatively you can provide your own SSL certificate [during installation](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-kubernetes-via-helm) or [via the Portainer UI](../../../../admin/settings/#ssl-certificate) after installation is complete.



If you need to access Portainer via HTTP on port `30777`, remove the `--set tls.force=true` option.




In this example, Portainer will be deployed to your cluster and assigned a Cluster IP, with an nginx Ingress Controller at the defined hostname. For more on Ingress options, refer to the list of [Chart Configuration Options](../../../../advanced/helm-chart-configuration-options.md).

```
helm upgrade --install --create-namespace -n portainer portainer portainer/portainer \
    --set service.type=ClusterIP \
    --set tls.force=true \
    --set image.tag=lts \
    --set ingress.enabled=true \
    --set ingress.ingressClassName=<ingressClassName (eg: nginx)> \
    --set ingress.annotations."nginx\.ingress\.kubernetes\.io/backend-protocol"=HTTPS \
    --set ingress.hosts[0].host=<fqdn (eg: portainer.example.io)> \
    --set ingress.hosts[0].paths[0].path="/"
```


If you need to access Portainer via HTTP, remove the `--set tls.force=true` option.




Using the following command, Portainer will be available at an assigned Load Balancer IP on port `9443` for HTTPS:

```
helm upgrade --install --create-namespace -n portainer portainer portainer/portainer \
    --set service.type=LoadBalancer \
    --set tls.force=true \
    --set image.tag=lts
```


By default, Portainer generates and uses a self-signed SSL certificate to secure port `9443`. Alternatively you can provide your own SSL certificate [during installation](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-kubernetes-via-helm) or [via the Portainer UI](../../../../admin/settings/#ssl-certificate) after installation is complete.



If you need to access Portainer via HTTP on port `9000`, remove the `--set tls.force=true` option.





If you want to explicitly set the target node when deploying the Helm chart on the CLI, include `--set nodeSelector.kubernetes\.io/hostname=<YOUR NODE NAME>` in your `helm install` command.


### Deploy using YAML manifests

Our YAML manifests support exposing Portainer via either NodePort or Load Balancer.



To expose via NodePort, you can use the following command (Portainer will be available on port `30777`  for HTTP and `30779` for  HTTPS):

```
kubectl apply -n portainer -f https://downloads.portainer.io/ce-lts/portainer.yaml
```


By default, Portainer generates and uses a self-signed SSL certificate to secure port `30779`. Alternatively you can provide your own SSL certificate [during installation](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-kubernetes-via-helm) or [via the Portainer UI](../../../../admin/settings/#ssl-certificate) after installation is complete.




To expose via Load Balancer, use the following command to provision Portainer at an assigned Load Balancer IP on port `9000` for HTTP and `9443` for HTTPS:

```
kubectl apply -n portainer -f https://downloads.portainer.io/ce-lts/portainer-lb.yaml
```


By default, Portainer generates and uses a self-signed SSL certificate to secure port `9443`. Alternatively you can provide your own SSL certificate [during installation](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-kubernetes-via-helm) or [via the Portainer UI](../../../../admin/settings/#ssl-certificate) after installation is complete.





If you want to explicitly set the target node when deploying using YAML manifests, run the following one-liner to "patch" the deployment, forcing the pod to always be scheduled on the node it's currently running on:


```
kubectl patch deployments -n portainer portainer -p '{"spec": {"template": {"spec": {"nodeSelector": {"kubernetes.io/hostname": "'$(kubectl get pods -n portainer -o jsonpath='{ ..nodeName }')'"}}}}}' || (echo Failed to identify current node of portainer pod; exit 1)
```

## Logging In

Now that the installation is complete, you can log into your Portainer Server instance. Depending on how you chose to expose your Portainer installation, open a web browser and navigate to the following URL:



```bash
https://localhost:30779/ or http://localhost:30777/
```

Replace `localhost` with the relevant IP address or FQDN if needed, and adjust the port if you changed it earlier.



```bash
https://<FQDN>/
```

Replace `<FQDN>` with the FQDN of your Portainer instance.



```bash
https://<loadbalancer IP>:9443/ or http://<loadbalancer IP>:9000/
```

Replace `<loadbalancer IP>` with the IP address or FQDN of the load balancer, and adjust the port if you changed it earlier.



You will be presented with the initial setup page for Portainer Server.


[setup.md](../setup.md)

