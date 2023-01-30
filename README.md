<h1>AWS WAF Configuration</h1>

<h2>Description</h2>
Project consists of implementing security configuration using a Web Application Firewall (WAF) to prevent unauthorized access to content saved in the cloud.
<br />


<h2>Utilities Used</h2>

- <b>Amazon Web Services</b>
- <b>AWS Windows Server 2016 EC2 Instance</b>

<h2>Configuring an S3 bucket:</h2>
AWS S3 stores data in buckets that are accessible from anywhere. In this project, I will create a storage server with a bucket that contains a file. This will be able to be accessed by anyone over the internet. The S3 service is first navigated to:<br/>
<img src="https://imagizer.imageshack.com/img922/8980/zwT2il.png" alt="Disk Sanitization Steps"/>
<br />
<br />
In the Buckets page, Create Bucket is selected:<br/>
<img src="https://imagizer.imageshack.com/img922/8027/LXe3Us.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The bucket is named and a region is assigned:<br/>
<img src="https://imagizer.imageshack.com/img924/8822/UW0iQ1.png" alt="Disk Sanitization Steps"/>
<br />
<br />
Turniung off the Block Public Access mark will make the bucket public:<br/>
<img src="https://imagizer.imageshack.com/img924/9423/OiWSbc.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The acknowledgement is checked:<br/>
<img src="https://imagizer.imageshack.com/img924/953/uocTcx.png" alt="Disk Sanitization Steps"/>
<br />
<br />
Create bucket is clicked:<br/>
<img src="https://imagizer.imageshack.com/img922/3801/30dx0O.png" alt="Disk Sanitization Steps"/>
<br />
<br />
Clicking the name of the newly created bucket accesses its page:<br/>
<img src="https://imagizer.imageshack.com/img924/1306/6pNMQH.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The upload option is selected to start uploading files to the bucket:<br/>
<img src="https://imagizer.imageshack.com/img922/2341/KAczDg.png" alt="Disk Sanitization Steps"/>
<br />
<br />
Add files is clicked and the index.html file is uploaded. Files can also be dragged and dropped:<br/>
<img src="https://imagizer.imageshack.com/img922/850/iBX2Ag.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The index.html file is checked and upload is selected:<br/>
<img src="https://imagizer.imageshack.com/img923/3091/NWKol5.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The file is verified as uploaded:<br/>
<img src="https://imagizer.imageshack.com/img923/9171/3XrIcQ.png" alt="Disk Sanitization Steps"/>
<br />
<br />

<h2>CloudFront Configuration:</h2>
CloudFront is a content delivery service that will be used to deliver the contents saved in the bucket. The process invloves creating a new distribution domain. After returning to the AWS console, CloudFront service is selected:<br/>
<img src="https://imagizer.imageshack.com/img923/7646/BOF6Gn.png" alt="Disk Sanitization Steps"/>
<br />
<br />
Create distribution is clicked to begin working with AWS CloudFront:<br/>
<img src="https://imagizer.imageshack.com/img922/6387/vOTdxD.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The distribution's origin domain name is entered:<br/>
<img src="https://imagizer.imageshack.com/img923/6174/cAv62g.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The default root object is defined with the name of the file uploaded to the index.html bucket. Create distribution is clicked. The origin domain name is made sure to match the name of the bucket created in the previous task:<br/>
<img src="https://imagizer.imageshack.com/img922/5797/aY1bRF.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The distribution is verified as created. The domain name is noted for later use. It can be noted that it takes some time for the distribution to change its status to Deployed:<br/>
<img src="https://imagizer.imageshack.com/img924/981/Pt0FbB.png" alt="Disk Sanitization Steps"/>
<br />
<br />

<h2>WAF Configuration:</h2>
The WAF will enable control over which traffic from web applications is permitted and blocked (in this case, CloudFront content), according to predefined rules. Only the EC2 will have access. All others will be blocked. First, the EC2 instance is verified as running:<br/>
<img src="https://imagizer.imageshack.com/img923/7253/0DzwYM.png" alt="Disk Sanitization Steps"/>
<br />
<br />
WAF & Shield is selected from the search bar:<br/>
<img src="https://imagizer.imageshack.com/img924/7946/pW0lpK.png" alt="Disk Sanitization Steps"/>
<br />
<br />
AWS Classic is switched to:<br/>
<img src="https://imagizer.imageshack.com/img924/5615/NnHNDj.png" alt="Disk Sanitization Steps"/>
<br />
<br />
IP addresses is navigated to and Create condition is clicked:<br/>
<img src="https://imagizer.imageshack.com/img923/9118/rXKaUA.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The condition is named Allowed-IP, and the region is set to Global (CloudFront). The IP address is set to the public IP of the EC2 server. Add IP address or range is clicked, then Create. It can be noted that the IP addresss of the EC2 server appears in the EC2 dashboard:<br/>
<img src="https://imagizer.imageshack.com/img922/3651/2liE6y.png" alt="Disk Sanitization Steps"/>
<br />
<br />
Create is clicked:<br/>
<img src="https://imagizer.imageshack.com/img922/7192/C0KVNW.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The IP match condition is verified as created. Web ACLs in the menu on the left is clicked to create a firewall rule:<br/>
<img src="https://imagizer.imageshack.com/img923/2570/84HNCf.png" alt="Disk Sanitization Steps"/>
<br />
<br />
Create web ACL is clicked:<br/>
<img src="https://imagizer.imageshack.com/img923/7158/hAEYzd.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The ACL is named AllowMe and the CloudFront distribution is set as the resource for association. It can be noted that the CloudFront resource name appears when the field is clicked:<br/>
<img src="https://imagizer.imageshack.com/img924/1188/u95Ava.png" alt="Disk Sanitization Steps"/>
<br />
<br />
In the create conditions window, it can be noted that the previously created Allow IP condition is listed:<br/>
<img src="https://imagizer.imageshack.com/img922/3403/trEG7d.png" alt="Disk Sanitization Steps"/>
<br />
<br />
Create rule is clicked:<br/>
<img src="https://imagizer.imageshack.com/img924/4214/lmEGQE.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The rule is named AllowMeRule and the regular rule type is assigned. Under Add conditions, the following are selected: does, originate from an IP address in, and Allow-IP. Create is then clicked:<br/>
<img src="https://imagizer.imageshack.com/img924/7587/a6d07F.png" alt="Disk Sanitization Steps"/>
<br />
<br />
In the create rules window the rule's action is set to Allow. Block all requests that don't match any rules is then clicked. Review and create is clicked:<br/>
<img src="https://imagizer.imageshack.com/img923/4849/K4RLgV.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The ACL configuration is verified and created:<br/>
<img src="https://imagizer.imageshack.com/img922/1184/rqiTDY.png" alt="Disk Sanitization Steps"/>
<br />
<br />

<h2>Verify WAF:</h2>
The EC2 instance is connected to via RDP. This process is described within previous projects. Internet Explorer is opened, and Don't use recommended settings is checked. The link is copied from CloudFront found in Networking & Content Delivery:<br/>
<img src="https://imagizer.imageshack.com/img923/346/hW4lrE.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The domain address of CloudFront is displayed. Continue to prompt is selected, and Add is clicked:<br/>
<img src="https://imagizer.imageshack.com/img924/6349/kImTwB.png" alt="Disk Sanitization Steps"/>
<br />
<br />
Add is clicked once again:<br/>
<img src="https://imagizer.imageshack.com/img923/7342/PXpU2o.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The same address is navigated within my personal computer. The access is blocked to the operation of the configured WAF:<br/>
<img src="https://imagizer.imageshack.com/img923/104/0oGcDK.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The RDP connection is disconnected:<br/>
<img src="https://imagizer.imageshack.com/img924/1250/ol6GeD.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The EC2 instance is stopped, and terminated:<br/>
<img src="https://imagizer.imageshack.com/img922/4951/TFvs9y.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The S3 bucket is also deleted:<br/>
<img src="https://imagizer.imageshack.com/img922/6706/8iXmiZ.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The cloudfront distribution is also disabled and deleted:<br/>
<img src="https://imagizer.imageshack.com/img923/9130/N77O0f.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The WAF & Shield service is navigated to. The AllowMe ACL is clicked. The rules tab is opened and Edit web ACL is clicked. The ACL is deleted:<br/>
<img src="https://imagizer.imageshack.com/img923/4136/qeD8Ru.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The rule is then edited, and the IP address is removed:<br/>
<img src="https://imagizer.imageshack.com/img924/3753/ZaCBkZ.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The AllowMeRule is clicked and deletedbr/>
<img src="https://imagizer.imageshack.com/img924/8531/PBAwec.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The Allowed-IP is deleted:<br/>
<img src="https://imagizer.imageshack.com/img922/2377/5vgKCQ.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The Web ACL is deleted:<br/>
<img src="https://imagizer.imageshack.com/img924/4723/RsvlY5.png" alt="Disk Sanitization Steps"/>
<br />
<br />

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
