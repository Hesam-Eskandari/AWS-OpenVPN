# AWS-OpenVPN
<h1>How To Build An Openvpn Server On AWS</h1>
This tutorial is under construction
<h2>Amazon Web Service</h2>
<p>With AWS you reserve a computer on Amazon cloud to build and run projects of yours or your company.</p> 
<p>There could be Several reasons to prefer a cloud computer to your personal one sitting on your desk. I could name a few:
  <ul>
    <li>If you need to run a service/project 24/7</li>
    <li>If you want to launch a service that requiers high internet bandwidth</li>
    <li>If you want to access to your projrct anywhere in the world and you don't want to carry your own computer everywhere</li>
    <li>If you want to run a business</li> 
  </ul>
  </p>
  
<p>
  A personal AWS account lets you benefit from a few free services under certain condisions. Look at the <a href="https://aws.amazon.com/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc">AWS Free Tier</a> website for more information regarding their offers. 
</p>
<h2>Launch A New Instance</h2>
<p>
  Making one instance that is always running is free for the first 12 months starting the second you make a new accound. Sign in to AWS Management Console, go to services, open EC2 dashboard and luanch a new instance. I chose an instance running ubuntu for the purpose of making an OpenVPN server. 
</p>
<p>
  In the security group section, click on edit security groups and add rule.
  <ul>
    <li>Type: SSH, Port: 22, Source: Anywhere</li>
    <li>Type: HTTP, Port: 80, Source: Anywhere</li>
    <li>Type: CustomTCP, Port: (your choice) 1194, Source: Anywhere</li>
    <li>Type: CustomUDP, Port: (your choice) 2525, Source: Anywhere</li>
  </ul>
</p>
<p>
  The key pairs you make is the key to access the sever instance you make. Download the key and a .pem file would be saved in your computer.  
</p>
<h3>Set Static IP</h3>
<p>
  We recommend you to set the server IP static. It would let you to connect to the instance with one public IP anytime. Go back to EC2 dashboard and click on the Elastic IP, choose the instance, click on the Associate Elastic IP in the Action, chose your instance and finish it. 
</p>
<h2> Connect Via SSH</h2>
You could connect to your launched instance from Ubuntu terminal with the .pem key file you downloaded or with Putty using a .ppk key file. To convert .pem to .ppk in Ubuntu use thie commend in therminal:
</p>

```
puttygen keyfile.pem -o keyfile.ppk
```

And in windows download the puttygen and convert the file.

<p> 
  I recommend to connect to the server in terminal if you are using Ubuntu and use putty if you are a Windows user. Go to your EC2 dashboard and click on Running Instances. You would find the instruction to connect to you instance via SSH by clicking on "Connect" button.
</p>

<h2>Install OpenVPN And Create Clients</h2>
You need to write down the public IP address of you instance before installing and using openvpn. It is the elastic IP you set.
<p>
  Connect to the instance and write the following command to install OpenVPN:
 </p>
 
 ```
 $ wget https://git.io/vpn -O openvpn-install.sh
 ```
 
 <p>Type the following command to set openvpn settings and create your first client
</p>

```
$ sudo bash openvpn-install.sh
```
<p> It will ask a few questions the first time you run this command.<br>
  <ul>
    <li>Use the public IP address of the instance</li>
    <li>Use the TCP costom port you made in security group (1194)</li>
    <li>Use Google as DNS</li>
  </ul>
  Then it will ask for the first client name and creates a ".ovpn" file for it in a directory and gives you the path to the directory. The next time you run the command above it would ask you to create or manage your clients. 
</p>
 
<h2>Download The ".ovpn" Files</h2>
 Use the commend bellow in Ubuntu terminal in your computer (not the server) to download the .ovpn client files you made.
 
 ```
 sudo scp -i /path1/keyFile.pem ubuntu@<PublicDNS>:/path2/clientFile.ovpn /path3
 ```
 
 <p> in the command above:
    <ul>
      <li>Path1 is the path to the keyFile.pem in your computer</li>
      <li>Path2 is the path to .ovpn file inthe server instance</li>
      <li>Path3 is the path in your computer that the .ovpn file would be downloaded</li>
    </ul>
 </p>
 
 <h2>Connect to OpenVPN</h2>
 <p>Now that you have the ovpn file you can connect to the server. Download the <a href="https://openvpn.net/community-downloads/">openvpn client</a> in your device, import the ovpn file (in the icon tray) and hit connect.
 </p>
 
 <h2>Manage OpenVPN</h2>
 If you have trouble connecting to VPN try to restart the OpenVPN service:
 
 ```
 $ sudo systemctl restart openvpn@server
 ```
 
 If you want to stop the service:
 
 ```
 $ sudo systemctl stop openvpn@server
 ```
 
 To start the OpenVPN service again:
 
 ```
 $ sudo systemctl stop openvpn@server
 ```
 
