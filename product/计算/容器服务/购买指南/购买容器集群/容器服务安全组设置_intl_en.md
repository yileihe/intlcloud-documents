Security has always been a major concern. By listing security as the top priority in product design, Tencent Cloud requires all its products to be fully isolated and provides multiple layers of security protection with the basic network. TKE is a typical example. It adopts [VPC](https://intl.cloud.tencent.com/document/product/215/535) as the underlying network of container services. This document describes the best practice of security group usage in TKE to help you select the most appropriate security group policy.

## Security Group
A security group is a virtual firewall capable of filtering stateful packets. As an important network security isolation mean provided by Tencent Cloud, it can be used to set network access control for one or more CVM instances. For more information, see [Security Group](https://intl.cloud.tencent.com/document/product/213/12452).

## Principles on Security Group Selection for TKE
1. Service pods are distributed on different nodes in a cluster. It is recommended to bind all CVM instances in one cluster to the same security group and not to add other instances to this security group.
2. The security group should grant only the minimum permission externally.
3. The following TKE rules need to be open to the internet:
 - Open the container pod network and cluster node network to the internet
 After a service access request reaches a node, the request is forwarded to a random pod of the service via the iptables rule set by the kube-proxy module. As a service pod is likely to be on another node, cross-node access occurs in this case. For example, the destination IPs of the access request include service pod IP, IP of other nodes in the cluster and IP of cbr0 bridge IP of cluster on the node. This requires the opposite node to allow access requests from the container pod network and cluster node network.
 - The corresponding container network and node network of the cluster should be opened to the internet if different clusters in the same VPC cannot communicate with one another.
 - Open port 22 to the internet on a node that required SSH login
 - Open ports 30000 - 32768 on a node to the internet
 In the access path, it is required to forward data packets to NodeIP: NodePort of the container cluster through CLB, where NodeIP is the CVM instance IP of a random node in the cluster, and NodePort is assigned by the container cluster by default when the service is created. The range of NodePort is between 30000 and 32768.
 The figure below uses public network access as an example:
![Public network access by CLB](https://main.qcloudimg.com/raw/0a237626a95174fd851052f49a0ff5b3.png)

## Security Group Configuration Template
It is recommended to configure the security group for the cluster using the security group template provided by TKE. The specific rules of the security group are as shown below:

Inbound rules:

| Protocol | Port | IP Range | Action | Description |
|:--------:|:---------:|:-------:|:--------:|:---------:|
|TCP|30000 - 32768|0.0.0.0/0| Allow | Allow TCP access to ports 30000 - 32768 by all IPs |
|UDP|30000 - 32768|0.0.0.0/0| Allow | Allow UDP access to ports 30000 - 32768 by all IPs |
|All |trafficALL|10.0.0.0/8|Allow | Allow access to the private network IP range of 10.0.0.0/8 |
|All |trafficALL|172.16.0.0/12|Allow | Allow access to the private network IP range of 172.16.0.0/12 |
|All| traffic ALL|192.168.0.0/16| Allow | Allow access to the private network IP range of 192.168.0.0/16 |
|TCP|22|0.0.0.0/0|Allow | Allow access to port 22 by requests from all IPs |
|All |trafficALL|0.0.0.0/0| Reject | If no existing rule is matched, the access is denied |

Outbound rules:

| Protocol | Port | IP Range | Action | Description |
|:--------:|:---------:|:-------:|:--------:|:---------:|
|All | trafficALL  |0.0.0.0/0  | Allow | Allow all rules |

Configuring this rule for container nodes can make the services in the cluster accessible in different access methods.
For more information on the access methods for services in the cluster, see [Service Access Method Settings](https://intl.cloud.tencent.com/document/product/457/9098).

