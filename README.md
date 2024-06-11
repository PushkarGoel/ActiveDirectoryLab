<h1>Active Directory Lab</h1>

<h2>Description</h2>

This repo includes steps for setting up an Active Directory (AD) home lab to learn and experiment with Windows Server and AD functionalities. This guide will walk you through the process of creating a virtualized environment using VirtualBox, installing Windows Server, and configuring Active Directory services. By the end of this setup, you will have a functional AD environment for testing and educational purposes.

<h2>Languages and Utilities Used</h2>
<h4> Languages: </h4>
- Powershell<br/>
<h4> Utilities: </h4>
- VirtualBox<br/>
&nbsp;  &nbsp; &nbsp; &nbsp; Windows Server ISO<br/>
&nbsp;  &nbsp; &nbsp; &nbsp; Windows 10 Pro ISO<br/>
<h2>Environments Used</h2>

- A host machine with enough resources to run VMs (At least 16gb recommended)
- Virtual Machines : VMs for Windows Server 2019 and Windows 10 Pro

<h2> Lab Walkthrough</h2>

<p >
<b>1.</b> Download and install virtal box <br/>
<br />
Then download ISOs for Windows Server 2019 and Windows 10 based on your host system <br/>
  Link for Windows server ISO : https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019<br/>
  Link for Windows 10 ISO : https://www.microsoft.com/en-us/software-download/windows10ISO<br/>
</p>
<br />
<p>
  <b>2.</b> Created a new vm for the Windows 2019 Server in virtual box with minimum 4 GB of ram and 40 gb of space. <br/>
  I also created two network adapter , one internal and one a NAT (for internet) <br/>
  Opened the created vm and then mount the downloaded Windows 2019 ISO. I then installed the "Windows Server 2019 Datacenter (Desktop Experience)"<br/>
  <img src="https://i.imgur.com/dTgXVwS.png" height="80%" width="80%" alt="AD LAB"/> <br/>
</p>
<br/>
<p>
  <b>3.</b> Changed the names of the internal and NAT adapters to <b>_INTERNAL_</b> and <b>_INTERNET_</b> respectively to identfiy them easily <br/>
  I then set up the IP address for internal adapter. (Did not setup IP for internet adapter as its gonna handled by host DHCP)<br/>
  <img src="https://i.imgur.com/bgmO8Cb.png" height="80%" width="80%" alt="AD LAB"/> <br/>
  
</p>
<br/>
<p>
  <b>4.</b> Created a domain - "mydomain.com" for the windows server by adding active directory feature using server manager <br/>
    <img src="https://i.imgur.com/s2S0GmF.png" height="80%" width="80%" alt="AD LAB"/> <br/>
  I then went to Active Directory users and Computer and created a new organasational unit called ADMINS and then created an admin user for myself <br/>
  <img src="https://i.imgur.com/dlPkhq6.png" height="80%" width="80%" alt="AD LAB"/> <br/>
  
</p>
<br />
<p>
  <b>5.</b> I then added routing feature into server through server management to allow access to internet from server. After adding feature, I confgured the routing through Routing and Remote access toolbar present in Tools menu <br/>
    <img src="https://i.imgur.com/vMOQm8Z.png" height="80%" width="80%" alt="AD LAB"/> <br/>
    <img src="https://i.imgur.com/XRn1wiS.png" height="80%" width="80%" alt="AD LAB"/> <br/>
</p>
<br />
<p>
<b>6.</b> After that, I set up DHCP server for the internal netowrk so that it can assign IP addresses to client connecting to the created server. I first added the DHCP feature to server and then configured it by going to tools>DHCP <br/>
  I set up the IP address from 192.16.1.100 - 192.16.1.200 as I was just doing a practice run, but we can set it as per our requirements. I also set up the lease duration as 8 days(default) but can reduce it or increase it as per requirements <br/>
    <img src="https://i.imgur.com/TwHilsa.png" height="80%" width="80%" alt="AD LAB"/> <br/>  
</p>
<br />
<p>
  <b>7.</b> Now I setup the windows 10 client vm which would be connecting to the internet via this server. <br/>
  Created a new vm for the Windows 10  in virtual box (with minimum 4 GB of ram and 40 gb of space). <br/>
  Changed its network adapter to same internal adapter as windows server so that they can access each other <br/>
    <img src="https://i.imgur.com/NE4BnjT.png" height="80%" width="80%" alt="AD LAB"/> <br/>
</p>
<br />
<p>
  <b>8.</b> I went into the client vm and then checked that I am able to access internet and the internal domain - "mydomain.com" <br/>
  <img src="https://i.imgur.com/G3GnqVF.png" height="80%" width="80%" alt="AD LAB"/> <br/>
</p>
<br />
<p>
  <b>9.</b> Now that we have a client and server, I wanted to test out AD features by logging as different users. So I created a powershell script for creating users (to reduce the manual efforts) <br/>
  The powershell script is in the repo : <add link> <br/>
  For that, I first created a list of random names and stored them in a text file <br/>
    <img src="https://i.imgur.com/jVUt2HG.png" height="50%" width="40%" alt="AD LAB"/> <br/> 
  I then fed them into my powershell script which created a new organizational unit _USERS and then added users into it with name  first letter of first name followed by the last name from the names in the list<br/>
  <img src="https://i.imgur.com/FkpjitE.png" height="80%" width="80%" alt="AD LAB"/> <br/>
  Thus a number of users were created in our domain. These accounts represent company accounts created for employees<br/>
  <img src="https://i.imgur.com/vw2oW3S.png" height="60%" width="40%" alt="AD LAB"/> <br/>
</p>
<br />
<p>
  <b>10.</b> After creating the accounts, I went to windows 10 vm and changed its domain to mydomain.com (This feature is NOT in windows home and that is why windows 10 pro is needed) <br/>
  To do that, went  to system properties and clicked on rename this PC (advanced). Changed domain to mydomain.com and username to USER1 <br/>
    <img src="https://i.imgur.com/1tvZudP.png" height="80%" width="80%" alt="AD LAB"/> <br/>
</p>
<br />
<p>
  <b>11.</b> Now we can login as any user we created in the windows server AD in the windows 10 vm
  <img src="https://i.imgur.com/nmk4tRv.png" height="80%" width="80%" alt="AD LAB"/> <br/>
</p>
<br />
<p> This simulates how an organization can set up AD on its system so that any employee with releavnt account can sign in to it</p>
