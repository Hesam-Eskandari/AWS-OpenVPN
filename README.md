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
  A personal AWS account lets you benefit from a few free services under certain condisions. Look at the [AWS Free Tier](https://aws.amazon.com/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc) website for more information regarding their offers. 
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
