# Kube DOOM in a VMware Cloud Foundation 9 All-Apps tenant organization 
## Kill Kubernetes pods using Id's Doom!

The next level of chaos engineering is here! Kill pods inside your Kubernetes
cluster by shooting them in Doom!

This enables the deployment of the excellent doom fork 
[storax/kubedoom](https://github.com/storax/kubedoom) on the VMware Cloud Foundation 9 
private cloud stack using an all-apps organization with VKS and VPCs.

![DOOM](assets/doom.png)

## Running Locally

In order to run locally you will need to

1. Run the kubedoom container
2. Attach a VNC client to the appropriate server and port (5901)

### Attaching a VNC Client

Now start a VNC viewer and connect to `vnc-server:5901`. The password is `idbehold`:
```console
$ vncviewer viewer vnc-server:5901
```
You should now see DOOM! Now if you want to get the job done quickly enter the
cheat `idspispopd` and walk through the wall on your right. You should be
greeted by your pods as little pink monsters. Press `CTRL` to fire. If the
pistol is not your thing, cheat with `idkfa` and press `5` for a nice surprise.
Pause the game with `ESC`.

### Running Kubedoom inside VKS with VPC and a Load Balancer

Create a Kubernetes Guest Cluster in VCF Automation portal as described in my 
[blog](https://adrian.heissler.at/2026/03/deploy-virtual-machines-and-kubernetes-workloads-in-a-vcf-automation-9-all-apps-organization/). 

This will spin up a 2 node cluster inside VKS, with port 5900 exposed from
the worker node. Then run kubedoom inside the cluster by applying the manifest
provided in this repository:

```console
$ kubectl apply -k manifest/
namespace/kubedoom created
serviceaccount/kubedoom created
clusterrole.rbac.authorization.k8s.io/kubedoom created
clusterrolebinding.rbac.authorization.k8s.io/kubedoom created
service/kubedoom created
deployment.apps/kubedoom created
```

To connect run:
```console
$ vncviewer viewer vnc-server:5901
```

This setup has been tested with VMware Cloud Foundation 9.0.2.
