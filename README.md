# Azure Architect Technology Implement Monitor Azure Infrastructures


## Site to Site VPN Connection

Suppose you want to establish a secure connection from your machine to a machine inside a VN using its private IP, you need to use a **Site to Site VPN** connection.

- create a VM *demovm* inside a VN *azure-network/subnetA*. Make sure the IP is None. North Europe location. Intall IIS 
<img src="/pictures/sts.png" title="site to site"  width="1000">

- inside *azure-network*, create a Gateway Subnet. Leave defaults. North Europe location
<img src="/pictures/sts1.png" title="site to site"  width="1000">

- create a Virtual Network Gateway *sitegateway*. North Europe location
<img src="/pictures/sts2.png" title="site to site"  width="500">

- create a VM *companyvm* inside a VN *company-network/subnetA*. East US location
<img src="/pictures/sts3.png" title="site to site"  width="500">
<img src="/pictures/sts31.png" title="site to site"  width="1000">

- on *companyvm*, install Remote access. Choose **Routing** and **DirectAccess** and VPN
<img src="/pictures/sts4.png" title="site to site"  width="1000">
<img src="/pictures/sts41.png" title="site to site"  width="1000">

- on *companyvm*, install getting started wizard. Choose **Deploy VPN only**.
<img src="/pictures/sts5.png" title="site to site"  width="1000">
<img src="/pictures/sts51.png" title="site to site"  width="1000">

- choose **Configure and Enable Routing and Remote Access**. Then **Custom Configuration**. Then **Demand Dial Connections** and **LAN Routing**. Then click **Start Service**
<img src="/pictures/sts52.png" title="site to site"  width="1000">
<img src="/pictures/sts53.png" title="site to site"  width="1000">
<img src="/pictures/sts54.png" title="site to site"  width="1000">

- create a **Local Network Gateway**. Use the IP of *companyvm* as well as the address space of *company-network*. Choose same location as the *sitegateway*.
<img src="/pictures/sts6.png" title="site to site"  width="500">

- on *sitegateway*, add a connection
<img src="/pictures/sts61.png" title="site to site"  width="500">
<img src="/pictures/sts62.png" title="site to site"  width="500">

Currently, on **Properties**, the status is *Not Connected* and in **Overview**, the Data is 0 bytes.
<img src="/pictures/sts63.png" title="site to site"  width="1000">

- on *companyvm*, on **Routing and Remote Access**, choose **New Demand-dial interface**. Give name *Azure*. Choose public IP of *sitegateway*
<img src="/pictures/sts7.png" title="site to site"  width="1000">
<img src="/pictures/sts71.png" title="site to site"  width="1000">
<img src="/pictures/sts72.png" title="site to site"  width="1000">
<img src="/pictures/sts73.png" title="site to site"  width="1000">
<img src="/pictures/sts74.png" title="site to site"  width="1000">

- on *companyvm*, on **Routing and Remote Access**, add a destination. Choose network range of *azure-network* 10.1.0.0/16. Then connect and see that you get an error.
<img src="/pictures/sts8.png" title="site to site"  width="1000">
<img src="/pictures/sts81.png" title="site to site"  width="1000">

- on *companyvm*, on **Routing and Remote Access**, right-click on properties, then **Security** tab, then preshared-key. See that the connection now works.
<img src="/pictures/sts82.png" title="site to site"  width="1000">
<img src="/pictures/sts83.png" title="site to site"  width="1000">
<img src="/pictures/sts84.png" title="site to site"  width="1000">
