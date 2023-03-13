<p align="center">
<img src="https://i.imgur.com/qIISe9r.jpg" alt="DNS"/>
</p>

<h1>Building Intuition for DNS</h1>
In this tutorial, we will be experimenting with DNS to help us gain a better understanding of DNS. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- DNS

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)

<h2> List of Prerequisites </h2>

- Active Directory running in Azure on a Virtual Machine
- A client machine running in Azure on a Virtual Machine
- Both can be built following this lab: <a href="https://github.com/galexwade/configure-ad">On-premises Active Directory Deployed in the Cloud (Azure)</a>

<h2>Actions and Observations</h2>

<!--- Step 1 -->
<p>
In this lab, we will be inspecting DNS A-Records on the server. A-Records are hostname to IP address mappings. We are going to create an A-Record on the Domain Controller for "mainframe" and have it point to the Domain Controller's private IP address. If we try to ping mainframe without setting the DNS record it will not work. When we ping "mainframe", the Client Machine is checking the DNS cache, the local host file and the DNS server. To create an A-Record go to Active Directory -> Tools -> DNS -> DC-1 -> Forward Lookup Zone -> mydomain.com -> right click and create a new A-Record, and title it "mainframe". If we go back to the Client Machine and ping mainframe, we will get a reply:
</p>
<p>
<img src="https://i.imgur.com/jNO0ZjT.png" height="80%" width="80%" alt="DNS Manager"/>
</p>
<p>
<img src="https://i.imgur.com/nChmbDf.png" height="80%" width="80%" alt="Command Line Prompt"/>
</p>
<br />

<!--- Step 2 -->
<p>
Now let's work with the Local DNS Cache. We will change the record address of "mainframe" to 8.8.8.8, and if we go back to the Client Machine it will still ping the old address even though we changed it. This is because we have to flush the DNS with the command "ipconfig /flushdns". This will clear the DNS cache, and when we attempt to ping mainframe again, the address of the new record will show:
</p>
<p>
<img src="https://i.imgur.com/spi5Zym.png" height="80%" width="80%" alt="DNS Manager Mainframe Properties"/>
</p>
<p>
<img src="https://i.imgur.com/vYWk77u.png" height="80%" width="80%" alt="Command Line Prompt"/>
</p>
<br />

<!--- Step 3 -->
<p>
Now let's configure a CNAME record that points the host "search" to "www.google.com". If we ping "search", we will not be able to find the host. We have to go back into the DNS tool on the Domain Controller and create a CNAME record "search". Once created and we ping "search", it will ping Google's URL:
</p>
<p>
<img src="https://i.imgur.com/bJyHJuA.png" height="80%" width="80%" alt="DNS Manager"/>
</p>
<p>
<img src="https://i.imgur.com/Qoy5nn4.png" height="80%" width="80%" alt="Command Line Prompt"/>
</p>
<br />
