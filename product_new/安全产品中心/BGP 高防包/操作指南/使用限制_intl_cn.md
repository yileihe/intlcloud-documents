## 防护对象限制
BGP 高防包仅适用于腾讯云产品，包含云服务器、负载均衡、黑石物理服务器、NAT 网关等。

## 接入限制
BGP 高防包仅支持绑定同一地域内的腾讯云公网 IP。

## 黑白名单配置限制
- DDoS 黑白 IP 名单之和最多支持添加100个 IP 地址。
- CC 黑白 IP 名单分别最多支持添加50个 IP 地址。
- CC URL 白名单最多支持添加50个 URL。

## 地域限制
BGP 高防包只能绑定同一地域内的腾讯云设备，目前开放购买的地域包括：华北（北京）、华东（上海）、华南（广州）。
BGP 高防包在不同地域提供的高防能力请参考如下表格：
<table>
     <tr>
         <th>类型</th>  
         <th>地区</th>  
         <th>保底防护</th>  
         <th>弹性防护</th> 
		 <th>最大防护能力</th> 
     </tr>
	 <tr>
         <td   rowspan="3">独享包</td>  
         <td>广州</td>  
         <td>5Gbps - 50Gbps</td>  
         <td>30Gbps - 100Gbps</td>
		 <td>100Gbps</td>
     </tr> 
	 <tr>
         <td>北京</td>  
         <td>5Gbps - 50Gbps</td>  
         <td>30Gbps - 100Gbps</td>
		 <td>100Gbps</td>
     </tr>
	 <tr>
         <td>上海</td>  
         <td>5Gbps - 100Gbps</td>  
         <td>30Gbps - 300Gbps</td>
		 <td>300Gbps</td>
     </tr>
     </tr>
	 <tr>
         <td   rowspan="3">共享包</td>  
         <td>广州</td>  
         <td   rowspan="3"><li>20Gbps</li><li>50Gbps</li><li>100Gbps</li></td>  
         <td>30Gbps - 100Gbps</td>
		 <td>100Gbps</td>
     </tr> 
	 <tr>
         <td>北京</td>  
         <td>30Gbps - 100Gbps</td>
		 <td>100Gbps</td>
     </tr>
	 <tr>
         <td>上海</td>
         <td>30Gbps - 300Gbps</td>
		 <td>300Gbps</td>
    </tr>
		
		 
</table>

>?高防包支持境外区域，包括中国香港、新加坡、韩国首尔、日本东京、美西硅谷。目前仅白名单用户可以购买，如有防护需求，请 [联系我们](https://intl.cloud.tencent.com/support) 进行咨询或 [提交工单](https://console.cloud.tencent.com/workorder/category) 申请。
