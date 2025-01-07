<p align="center">
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h2>osTicket - Prerequisites and Installation</h2>
<p>This project involves configuring all the prerequisites and installing osTicket. The setup was completed on a Windows 10 Virtual Machine that I created in Azure. You can find the installation files used in this project <a href="https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD">here</a>.</p>

<h2>Environments and Technologies Used</h2>
<ul>
  <li>Microsoft Azure</li>
  <li>Virtual Machines</li>
  <li>Remote Desktop</li>
  <li>MySQL</li>
  <li>Internet Information Services (IIS)</li>
</ul>

<h2>Operating Systems Used</h2>
<ul>
  <li>Windows 10</li>
</ul>

<h2>List of Prerequisites</h2>
<ul>
  <li><b>PHP manager for IIS</b> - ensures PHP is correctly configured to run IIS</li>
  <li><b>Rewrite module</b> - facilitates URL rewriting and redirect users to URLs</li>
  <li><b>VC_redist.x86</b> (redistributable) - osTicket relies on libraries that are part of Microsoft Visual C++ and ensures the program runs smoothly</li>
  <li><b>MySQL</b> - for storing data into databases</li>
  <li><b>HeidiSQL</b> - interface for accessing MySQL</li>
</ul>

<h3>💻 Azure Resource Group and Virtual Machine Setup</h3>

<details>
  <summary>📦 Creating the Resource Group</summary>
  <p>I'll navigate to the Azure Portal and click or search for `Resource Groups`.</p>
  <img src="https://github.com/user-attachments/assets/c5d5eee0-7df2-4cf4-9a71-396e7c7ebb89" alt="Creating Resource Group"/>
  <p>On the Resource Group page I'll click `Create` at the top-left.</p>
  <img src="https://github.com/user-attachments/assets/8d197474-33c9-4162-ad74-392986fb3249" alt="Creating Resource Group"/>
  <p>I'll select my Azure subscription and name the Resource Group `rg-osticket`, set the Region to `East US 2`, then click `Review + Create`.</p>
  <img src="https://github.com/user-attachments/assets/96334a91-91c2-4102-8893-b89c0442ec91" alt="Review and Create Resource Group"/>
  <p>And finally, click `Create` again.</p>
  <img src="https://github.com/user-attachments/assets/74840e04-9959-4307-9a63-2a1ee6f5a151" alt="Finalizing Resource Group Creation"/>
  <p>The Resource Group has been created. In the next section, I will set up the virtual machine.</p>
</details>

<details>
  <summary>💻 Creating the Virtual Machine</summary>
  <p>On the Azure Portal, I'll search for `Virtual Machines`.</p>
  <img src="https://github.com/user-attachments/assets/7b49b5b6-0448-48ad-9a98-740b48903939" alt="Searching for Virtual Machines"/>
  <p>On the Virtual Machine page, I'll click `Create` on the top-left, then select `Azure Virtual Machine`.</p>
  <img src="https://github.com/user-attachments/assets/62e95754-35bc-4334-ab1b-651e15280ebd" alt="Creating Virtual Machine"/>
  <p>On the create page, I'll select the Resource Group that I just created `rg-osticket`, and name the VM `osticket-vm`.</p>
  <img src="https://github.com/user-attachments/assets/ae2eb56f-68f8-47bc-83ca-92dad2c922fe" alt="Configuring Virtual Machine"/>
  <p>I'll select `Windows 10 Pro (22H2)` as the image.</p>
  <img src="https://github.com/user-attachments/assets/5feef9a2-d693-4c2e-9dc9-8e02fc450eb1" alt="Selecting Windows 10 Image"/>
  <p>Then I'll select `Standard_D2s_v4 - 2vcpus, 8 GiB memory` as the VM size.</p>
  <img src="https://github.com/user-attachments/assets/0425cced-59c7-4604-a743-b7d2526b8e1e" alt="Selecting VM Size"/>
  <p>Enter a username and password, agree to the licensing terms, and leave all other settings, such as disk, network, and others, at their default values. Click `Review + Create`, then click `Create`.</p>
  <img src="https://github.com/user-attachments/assets/b3c8c8b5-fd4d-40b9-8d3b-bf2641681533" alt="Review and Create Virtual Machine"/>
  <p>The VM has been created.</p>
  <img src="https://github.com/user-attachments/assets/a14f14e0-09e8-47dc-a43b-1b3aeee4de06" alt="Virtual Machine Created"/>
</details>

<details>
  <summary>💻 Connect to the VM via RDP</summary>
  <p>Now that the VM has been created, I'll connect to it using RDP. To do this, I need the Public IP Address. In the Azure Portal, navigate to Virtual Machines, select `osticket-vm`, and copy the Public IP Address.</p>
  <img src="https://github.com/user-attachments/assets/0acc73fc-c07d-412f-a6ad-708f9902ab3a" alt="Copying Public IP Address"/>
  <p>On my Host Machine, I'll click `Start` and type `Remote Desktop`, then click `Remote Desktop Connection`.</p>
  <img src="https://github.com/user-attachments/assets/4999dad2-8aee-4acb-867d-769651b2696e" alt="Opening RDP"/>
  <p>I'll click `Show Options`, input the IP Address and username, then click `Connect`.</p>
  <img src="https://github.com/user-attachments/assets/1042ae72-10b6-43e7-b60e-af909c1fb8e2" alt="Connecting to the VM"/>
  <p>Input the password and click `OK`.</p>
  <img src="https://github.com/user-attachments/assets/c66072ec-cea3-4d64-aed9-45d87627e9cd" alt="Entering Password"/>
  <p>Click `Yes` to trust the certificate.</p>
  <img src="https://github.com/user-attachments/assets/f1eeecb0-1463-424c-99fd-918f923e5895" alt="Trusting Certificate"/>
  <p>I'm now logged into the VM.</p>
  <img src="https://github.com/user-attachments/assets/a14f14e0-09e8-47dc-a43b-1b3aeee4de06" alt="VM Logged In"/>
</details>

<h3>🎫 osTicket Installation Steps</h3>
<p>For this section, I downloaded a zip file that contains all the required installation files and then simply extracted the folder onto the desktop. The installation zip can be found <a href="https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD" target="_blank">here</a>.</p>

<details>
  <summary>⚙️ Install / Enable Internet Information Services (IIS) with CGI</summary>
  <p>To enable IIS, navigate to `Control Panel` -> `Programs` -> `Programs and Features`. Then click `Turn windows features on or off`.</p>
  <img src="https://github.com/user-attachments/assets/cc6e340c-cc45-429f-9cc0-ed4709f51623" alt="IIS Setup"/>
  <p>Select `Internet Information Services` then expand it and navigate to `World Wide Web Services` -> `Application Development Features` and check `CGI`. Then click `OK`. When the installation completes, click `Close`.</p>
  <img src="https://github.com/user-attachments/assets/03eb17c6-727b-4b31-83a0-636b65e0c3e8" alt="CGI Setup"/>
</details>

<!-- Continue modifying in the same style... -->
