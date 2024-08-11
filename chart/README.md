# sulfoxide-lead

![Version: 1.2.0](https://img.shields.io/badge/Version-1.2.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 0.1.0](https://img.shields.io/badge/AppVersion-0.1.0-informational?style=flat-square)

Helm chart to deploy EKS Bootstrap components includingg CSI (EBS and EFS) and LoadBalancer drivers

## Requirements

| Repository | Name | Version |
|------------|------|---------|
| https://aws.github.io/eks-charts | aws-load-balancer-controller | 1.8.2 |
| https://kubernetes-sigs.github.io/aws-ebs-csi-driver | aws-ebs-csi-driver | 2.33.0 |
| https://kubernetes-sigs.github.io/aws-efs-csi-driver | aws-efs-csi-driver | 3.0.8 |

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| aws-ebs-csi-driver | object | `{"controller":{"extraVolumeTags":{"<<":{"atomi.cloud/layer":"1","atomi.cloud/platform":"sulfoxide","atomi.cloud/service":"lead"},"atomi.cloud/module":"ebs-controller"},"loggingFormat":"json","podAnnotations":{"<<":{"atomi.cloud/layer":"1","atomi.cloud/platform":"sulfoxide","atomi.cloud/service":"lead"},"atomi.cloud/module":"ebs-controller"},"podLabels":{"<<":{"atomi.cloud/layer":"1","atomi.cloud/platform":"sulfoxide","atomi.cloud/service":"lead"},"atomi.cloud/module":"ebs-controller"},"replicaCount":2,"resources":{"limits":{"cpu":"250m","memory":"512Mi"},"requests":{"cpu":"128m","memory":"256Mi"}},"serviceAccount":{"annotations":{"eks.amazonaws.com/role-arn":"role"},"create":true,"name":"ebs-controller"},"topologySpreadConstraints":[{"labelSelector":{"matchLabels":{"<<":{"atomi.cloud/layer":"1","atomi.cloud/platform":"sulfoxide","atomi.cloud/service":"lead"}}},"maxSkew":1,"topologyKey":"topology.kubernetes.io/zone","whenUnsatisfiable":"ScheduleAnyway"}]},"customLabels":{"<<":{"atomi.cloud/layer":"1","atomi.cloud/platform":"sulfoxide","atomi.cloud/service":"lead"},"atomi.cloud/module":"ebs-controller"},"storageClasses":[]}` | AWS EBS CSI Driver configuration. See [AWS EBS CSI Driver Helm Chart](https://github.com/kubernetes-sigs/aws-ebs-csi-driver/blob/master/docs/install.md) |
| aws-efs-csi-driver | object | `{"controller":{"create":true,"podAnnotations":{"<<":{"atomi.cloud/layer":"1","atomi.cloud/platform":"sulfoxide","atomi.cloud/service":"lead"},"atomi.cloud/module":"efs-controller"},"resources":{"limits":{"cpu":"250m","memory":"512Mi"},"requests":{"cpu":"128m","memory":"256Mi"}},"serviceAccount":{"annotations":{"eks.amazonaws.com/role-arn":"role"},"create":true,"name":"efs-controller"}},"replicaCount":2,"storageClasses":[]}` | AWS EFS CSI Driver configuration. See [AWS EFS CSI Driver Helm Chart](https://github.com/kubernetes-sigs/aws-efs-csi-driver/tree/master) |
| aws-load-balancer-controller | object | `{"additionalLabels":{"<<":{"atomi.cloud/layer":"1","atomi.cloud/platform":"sulfoxide","atomi.cloud/service":"lead"},"atomi.cloud/module":"elb-controller"},"clusterName":"name","podAnnotations":{"<<":{"atomi.cloud/layer":"1","atomi.cloud/platform":"sulfoxide","atomi.cloud/service":"lead"},"atomi.cloud/module":"elb-controller"},"podLabels":{"<<":{"atomi.cloud/layer":"1","atomi.cloud/platform":"sulfoxide","atomi.cloud/service":"lead"},"atomi.cloud/module":"elb-controller"},"replicaCount":2,"resources":{"limits":{"cpu":"250m","memory":"512Mi"},"requests":{"cpu":"62.5m","memory":"128Mi"}},"serviceAccount":{"annotations":{"eks.amazonaws.com/role-arn":"role"},"create":true,"name":"elb-controller"},"serviceMonitor":{"enabled":true},"topologySpreadConstraints":[{"labelSelector":{"matchLabels":{"<<":{"atomi.cloud/layer":"1","atomi.cloud/platform":"sulfoxide","atomi.cloud/service":"lead"}}},"maxSkew":1,"topologyKey":"topology.kubernetes.io/zone","whenUnsatisfiable":"ScheduleAnyway"}]}` | AWS LoadBalancer Controller configuration. See [AWS LoadBalancer Controller Helm Chart](https://github.com/aws/eks-charts/tree/master/stable/aws-load-balancer-controller) |
| clusterName | string | `"name"` | Cluster name for the EKS cluster |
| modules | object | `{"ebs":"ebs-controller","efs":"efs-controller","elb":"elb-controller"}` | Module labels and annotations, following Service Tree for each EKS plugin |
| role | string | `"role"` | Role ARN for IRSA for service account |
| serviceTree | object | `{"layer":"1","platform":"sulfoxide","service":"lead"}` | AtomiCloud Service Tree. See [ServiceTree](https://atomicloud.larksuite.com/wiki/OkfJwTXGFiMJkrk6W3RuwRrZs64?theme=DARK&contentTheme=DARK#MHw5d76uDo2tBLx86cduFQMRsBb) |
| tags | object | `{"atomi.cloud/layer":"1","atomi.cloud/platform":"sulfoxide","atomi.cloud/service":"lead"}` | Kubernetes labels and annotations, following Service Tree |
| zoneSpread.config.image | string | `"public.ecr.aws/eks-distro/kubernetes/pause:3.7"` |  |
| zoneSpread.config.podSecurityContext | object | `{"fsGroup":1000,"runAsGroup":1000,"runAsNonRoot":true,"runAsUser":1000}` | PodSecurityContext for zone-spread pod |
| zoneSpread.config.resources | object | `{"limits":{"cpu":"125m","memory":"128Mi"},"requests":{"cpu":"0","memory":"0"}}` | Resources for zone-spread pod |
| zoneSpread.config.securityContext | object | `{"allowPrivilegeEscalation":false,"capabilities":{"drop":["ALL"]},"readOnlyRootFilesystem":true,"runAsGroup":1000,"runAsNonRoot":true,"runAsUser":1000}` | SecurityContext for zone-spread pod |
| zoneSpread.zones | object | `{"zone1":{"enabled":false,"replicas":1,"zone":"ap-southeast-1a"}}` | topology zones to deploy zone-spread pod to force node provisioning across zones |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
