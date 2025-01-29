# Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.1.9 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 5.0 |
| <a name="requirement_kubernetes"></a> [kubernetes](#requirement\_kubernetes) | >= 5.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 5.0 |

## Input Variables

The following table lists the input variables used in the Terraform code, along with their corresponding real values, descriptions, and types.

| Variable Name         | Value                                                     | Description                                                                      | Type             |
|-----------------------|-----------------------------------------------------------|----------------------------------------------------------------------------------|------------------|
| `cluster_name`         | `my-cluster-name`                                         | The name of the EKS cluster.                                                      | `string`         |
| `vpc_id`               | `vpc-0a1b2c3d4e5f67890`                                  | The VPC ID where the EKS cluster and other resources will be created.            | `string`         |
| `eks_subnets`          | `["subnet-0abcd123", "subnet-0abcd456", "subnet-0abcd789"]` | List of subnet IDs for EKS cluster deployment.                                   | `list(string)`   |
| `eks_version`          | `1.31`                                                    | Version of the EKS cluster to be created.                                        | `string`         |
| `eks_log_types`        | `["api", "audit", "authenticator", "controllerManager", "scheduler"]` | List of log types for EKS cluster logging.                                       | `list(string)`   |
| `node_policies`        | `["AmazonEKSWorkerNodePolicy", "AmazonEC2ContainerRegistryReadOnly", "AmazonEC2FullAccess", "AmazonEKS_CNI_Policy"]` | List of IAM policies attached to the EKS node role.                              | `list(string)`   |
| `eks_desired_size`     | `2`                                                       | Desired number of nodes in the EKS node pool.                                    | `number`         |
| `eks_max_size`         | `3`                                                       | Maximum number of nodes in the EKS node pool.                                    | `number`         |
| `eks_min_size`         | `1`                                                       | Minimum number of nodes in the EKS node pool.                                    | `number`         |
| `eks_disk_size`        | `20`                                                      | Disk size (in GB) for the EKS node pool instances.                               | `number`         |
| `eks_instance_types`   | `["t3.medium"]`                                           | Instance types for the EKS node pool.                                            | `list(string)`   |

## Output Variables

The following table lists the output variables used in the Terraform code, along with their corresponding real values, descriptions, and types.

| Output Name            | Value                                                   | Description                                                                      | Type             |
|------------------------|---------------------------------------------------------|----------------------------------------------------------------------------------|------------------|
| `eks_cluster_name`      | `aws_eks_cluster.eks_cluster.name`                      | The name of the EKS cluster created.                                             | `string`         |
| `eks_cluster_endpoint`  | `aws_eks_cluster.eks_cluster.endpoint`                  | The endpoint URL of the EKS cluster.                                             | `string`         |
| `eks_cluster_arn`       | `aws_eks_cluster.eks_cluster.arn`                       | The ARN of the EKS cluster.                                                      | `string`         |

| Resource Name                          | Resource Type                       | Description                                                                 |
|----------------------------------------|-------------------------------------|-----------------------------------------------------------------------------|
| [`aws_iam_role.eks_cluster_role`](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role)        | `aws_iam_role`                      | IAM Role for the EKS cluster allowing EKS service to assume the role.       |
| [`aws_iam_role_policy_attachment.eks_policy_attachment`](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | `aws_iam_role_policy_attachment`   | Attach IAM policies to the EKS cluster role.                                |
| [`aws_eks_cluster.eks_cluster`](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eks_cluster)          | `aws_eks_cluster`                   | The EKS cluster resource itself. Defines the cluster configuration.         |
| [`aws_iam_role.eks_node_role`](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role)           | `aws_iam_role`                      | IAM Role for the EKS node group allowing EC2 instances to join the cluster. |
| [`aws_eks_addon.vpc_cni`](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eks_addon)                | `aws_eks_addon`                     | EKS Addon for VPC CNI for networking within EKS pods.                       |
| [`aws_eks_addon.coredns`](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eks_addon)                | `aws_eks_addon`                     | EKS Addon for CoreDNS, which provides DNS services to the cluster.          |
| [`aws_eks_addon.kube_proxy`](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eks_addon)             | `aws_eks_addon`                     | EKS Addon for kube-proxy to enable network proxying within the EKS cluster.  |
| [`aws_vpc_endpoint.interface_endpoint`](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc_endpoint)  | `aws_vpc_endpoint`                  | VPC interface endpoints for AWS services like SSM, EC2, ECR, etc.           |
| [`aws_security_group.allow_endpoint`](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group)    | `aws_security_group`                | Security group to allow endpoint traffic within the VPC.                    |
| [`aws_security_group.eks_security_group`](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | `aws_security_group`                | Security group associated with the EKS cluster for controlling access.     |
| [`aws_security_group.eks_node_sg`](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group)       | `aws_security_group`                | Security group for EKS node group, allowing HTTPS and Kubernetes API traffic. |






