# Azure AKS cheatsheet

### HOW TO Understand
- https://learn.microsoft.com/en-us/azure/aks/
- https://github.com/Azure/AKS
    - issues - https://github.com/Azure/AKS/issues
    - projects - https://github.com/Azure/AKS/projects/1
    - images - https://github.com/Azure/AKS/tree/master/vhd-notes
- https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster
- https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster_node_pool
- https://github.com/kubernetes-sigs/cluster-api-provider-azure - https://capz.sigs.k8s.io/


### AKS checklist

- https://www.the-aks-checklist.com/

---
## Maintenance
### Upgrade k8s version

- https://kubernetes.io/releases/
- https://endoflife.date/kubernetes
- https://github.com/Azure/AKS/releases
- https://releases.aks.azure.com/
- https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster_node_pool#orchestrator_version

### Upgrade node pool image

- https://github.com/Azure/AKS/tree/master/vhd-notes
- https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-cluster#using-auto-upgrade
- https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster#automatic_channel_upgrade
- https://learn.microsoft.com/en-us/azure/aks/planned-maintenance
- https://learn.microsoft.com/en-us/azure/aks/use-system-pools?tabs=azure-cli#add-a-dedicated-system-node-pool-to-an-existing-aks-cluster
- https://learn.microsoft.com/en-us/azure/aks/node-updates-kured
- https://github.com/kubereboot/kured
- https://learn.microsoft.com/en-us/azure/aks/use-mariner
- https://learn.microsoft.com/en-us/azure/aks/cluster-configuration#deploy-an-aks-mariner-cluster-with-an-arm-template
- https://azure.microsoft.com/en-us/updates/generally-available-aks-support-for-ubuntu-2204/
- https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster_node_pool#os_sku

### k8s services HA

- node count > 3 - https://learn.microsoft.com/en-us/azure/aks/cluster-autoscaler#create-an-aks-cluster-and-enable-the-cluster-autoscaler
- deployment replica count > 3
- podAntiAffinity - https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#types-of-inter-pod-affinity-and-anti-affinity
- PodDisruptionBudget - https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-scheduler#voluntary-disruptions
- rollingStrategy - https://kubernetes.io/blog/2022/05/27/maxunavailable-for-statefulset/
- https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#example-1
- https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#when-should-you-use-a-liveness-probe
- nginx ingress-controler HA

---
## Features
### AutoScaling
- HPA vs Keda
- https://learn.microsoft.com/en-us/azure/aks/keda-about
- Functions on AKS - https://learn.microsoft.com/en-us/azure/azure-functions/functions-kubernetes-keda
- ACI - https://learn.microsoft.com/en-us/azure/aks/virtual-nodes-portal#create-an-aks-cluster

### Service Mesh
- open-service-mesh - https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-about
- LinkerD - https://linkerd.io/2.12/overview/
- Cilium Hubble - https://docs.cilium.io/en/v1.12/gettingstarted/hubble/
- https://isovalent.com/blog/post/2022-05-03-servicemesh-security/

### BYOCNI - eBPF
- https://learn.microsoft.com/en-us/azure/aks/azure-cni-overlay
- https://learn.microsoft.com/en-us/azure/aks/azure-cni-powered-by-cilium
- https://learn.microsoft.com/en-us/azure/aks/use-byo-cni?tabs=azure-cli
- https://docs.cilium.io/en/stable/gettingstarted/k8s-install-default/#k8s-install-standard
- https://docs.cilium.io/en/stable/concepts/networking/ipam/azure/#ipam-azure
- https://projectcalico.docs.tigera.io/maintenance/ebpf/install
- https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster#network_plugin
- https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster#ip_versions
- https://learn.microsoft.com/en-us/azure/aks/configure-kubenet-dual-stack?tabs=azure-cli%2Ckubectl

### AKS Bring your own CNI - part 2
- https://learn.microsoft.com/en-us/azure/aks/use-byo-cni?tabs=azure-cli
- https://www.tigera.io/blog/byocni-introducing-calico-cni-for-azure-aks
- https://docs.cilium.io/en/v1.12/gettingstarted/k8s-install-default/#k8s-install-quick
- https://www.youtube.com/watch?v=KvVWEmvsZqM
- https://www.youtube.com/watch?v=aLq3O3l2LF4&t=3110s

### GitOps
- Flux vs ArgoCD
- https://learn.microsoft.com/en-us/azure/azure-arc/kubernetes/conceptual-gitops-flux2?toc=https%3A%2F%2Flearn.microsoft.com%2Fen-us%2Fazure%2Faks%2Ftoc.json&bc=https%3A%2F%2Flearn.microsoft.com%2Fen-us%2Fazure%2Fbread%2Ftoc.json

### Storage
- https://learn.microsoft.com/en-us/azure/aks/csi-storage-drivers

### Security
- BYOK - https://learn.microsoft.com/en-us/azure/aks/azure-disk-customer-managed-keys
- proxy - https://learn.microsoft.com/en-us/azure/aks/http-proxy
- secrets - https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-driver
- https://learn.microsoft.com/en-us/azure/aks/managed-aad#disable-local-accounts
- https://learn.microsoft.com/en-us/azure/aks/cluster-configuration#node-restriction-preview
- https://learn.microsoft.com/en-us/azure/aks/cluster-configuration#oidc-issuer
- https://learn.microsoft.com/en-us/azure/aks/enable-fips-nodes
- https://learn.microsoft.com/en-us/azure/aks/use-kms-etcd-encryption?source=recommendations
- https://learn.microsoft.com/en-us/azure/aks/workload-identity-overview
- https://learn.microsoft.com/en-us/azure/aks/image-cleaner?tabs=azure-cli
- https://learn.microsoft.com/en-us/azure/aks/custom-certificate-authority
- https://learn.microsoft.com/en-us/azure/aks/certificate-rotation

### Private vs Public
- https://learn.microsoft.com/en-us/azure/aks/private-clusters
- https://learn.microsoft.com/en-us/azure/aks/command-invoke
- https://learn.microsoft.com/en-us/azure/aks/limit-egress-traffic?source=recommendations#restrict-egress-traffic-using-azure-firewall
- https://learn.microsoft.com/en-us/azure/aks/egress-outboundtype

### k8s operators and admission-controller
- https://github.com/nolar/kopf
- https://kopf.readthedocs.io/en/stable/
- https://sdk.operatorframework.io/docs/building-operators/golang/tutorial/
- https://operatorhub.io/
- https://www.baeldung.com/java-kubernetes-admission-controller
- https://bshayr29.medium.com/build-your-own-admission-controllers-in-kubernetes-using-go-bef8ba38d595
- https://dev.to/douglasmakey/implementing-a-simple-k8s-admission-controller-in-go-2dcg
- https://dev.to/ashokan/simple-validation-webhook-with-python-5bof

