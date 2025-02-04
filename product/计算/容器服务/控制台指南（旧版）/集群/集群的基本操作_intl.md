## Creating a Cluster
1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/ccs).
2. Click **Cluster** in the left navigation bar, and click **New** in the cluster list page.
![](https://main.qcloudimg.com/raw/b7bef172bccf2163ef4f52999702afc4.png)
3. Configure the basic cluster information.
 - **Cluster name**: The name of a cluster to be created, with a length limited to 60 characters.
 - **Billing method**: Both Prepaid and Postpaid are supported. For more information, please see [Billing Method](/doc/product/213/2180).
 - **Region**: Select a closest region based on your location. This helps minimize access latency and improve download speed.
 - **Availability zone**: Clusters in the same region are interconnected with each other through private network, but this is not the case for those distributed in different regions. The same region must be chosen for communication over private networks.
 - **Node network**: The system assigns the IP addresses within the node network address range to the CVMs in the cluster. For more information, please see [Network Configuration of Containers and Nodes](/doc/product/457/9083).
 - **Container network**: The system assigns the IP addresses within the container network address range to the containers in the cluster. For more information, please see [Network Configuration of Containers and Nodes](/doc/product/457/9083).
 - **Cluster description**: Information about cluster creation, which is displayed on the **Cluster Information** page.
![Alt text](https://main.qcloudimg.com/raw/b4ab931a23fb262bc043adaf162a40ab.png)

4. Select a model (all models with cloud disks as system disks are supported).
 - **Series**: **Series 1** and **Series 2** are available. <!--For more information, please see [Pod Types](/doc/product/213/7153#.E5.8F.AF.E7.94.A8.E5.AE.9E.E4.BE.8B.E7.B1.BB.E5.9E.8B2).-->
 - **Model**: For more information on how to select a model, please see [Select CVM Configuration Solution](/doc/product/213/2764#.E7.A1.AE.E5.AE.9A.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8.E9.85.8D.E7.BD.AE.E6.96.B9.E6.A1.88).
![Alt text](https://main.qcloudimg.com/raw/a8f59af5eb218c66cf1481e35dd6403e.png) 

5. Enter CVM configuration.
 - **System disk**: Always 50 GB.
 - **Data disk**: The increment is 10 GB. The maximum value is 4,000 GB.
 - **Public network bandwidth**: Two billing methods are available. <!--For more information, please see [Purchase Network Bandwidth](/doc/product/213/509).-->
 - **Bandwidth**: If you select **Assign public IP for free**, the system assigns a public IP at no cost. If there is no need, set bandwidth value to 0.
 - **Login method**: Three login methods are provided.
    i. **Set password**: Set a password as instructed.
	ii - **Immediately associate key**: A key pair is a pair of parameters generated by an algorithm, which makes it more secure to log in to a CVM than using a password.<!-- For more information, please see [SSH Key](/doc/product/213/503).-->
	iii. **Automatically generate password**: The automatically generated password is sent to you via the internal message.
 - **Security group**: It functions as a firewall and is used to set the network access control of CVMs. For more information, please see [Configure TKE Security Group](/doc/product/457/9084).
 - **Number of CVMs**: Select the number of CVMs.
![Alt text](https://main.qcloudimg.com/raw/4511911fa83275484cc58505fb079313.png)

6. The created cluster is displayed in the cluster list.

### Add a CVM
1. On the cluster list page, click **Add Node** on the right.
2. Set the **Network** to which the new CVM belongs, its **Model** and **Configuration information**.
   You may create CVMs in different subnets under different availability zones in the same region.
3. The new CVM can be found in the **ID/Node Name** column.


## Terminating a CVM
1. Click the **ID/Name** of a cluster on the cluster list page to enter the following page. Select a CVM to be terminated, and click **Remove** on the right.

2. When a prompt page that displays details of the node appears, click **OK** to remove the node.


## Viewing Node Information

1. Click **ID/Name**of the cluster in the cluster list.
2. Click **Node List** to view the cluster node list information.


## Logging in to a Node
Tencent Cloud CVM can be used as a node. For more information on login, please see [Log in to CVM](https://cloud.tencent.com/doc/product/213/5436).

## Creating a Namespace for a Cluster

1. Select **ID/Name** of a cluster on the cluster list page.
2. Click **Namespace List**, and then click **New Namespace**.
3. Enter the information and click **Submit**.

## Deleting a Namespace from a Cluster

1. Select **ID/Name** of a cluster on the cluster list page.
2. Click **Namespace List**, select a Namespace to be deleted, and click **Delete** on the right.
3. When a prompt page that displays details of the namespace appears, click **OK** to delete it.

>**Note**: 
>Deleting a namespace will terminate all the resources under this namespace. All the data will be cleared and cannot be recovered after termination. Please back up your data in advance.

