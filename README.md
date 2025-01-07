<p align="center">
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h2>osTicket - Prerequisites and Installation</h2>
<p>This project involves configuring all the prerequisites and installing osTicket. The setup was completed on a Windows 10 Virtual Machine that I created in Azure. You can find the installation files used in this project <a href="https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD">here</a>.</p>

<h2>🌍 Environments and Technologies Used 🌍</h2>
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

<h2>📝 List of Prerequisites</h2>
<ul>
  <li><b>PHP manager for IIS</b> - ensures PHP is correctly configured to run IIS</li>
  <li><b>Rewrite module</b> - facilitates URL rewriting and redirect users to URLs</li>
  <li><b>VC_redist.x86</b> (redistributable) - osTicket relies on libraries that are part of Microsoft Visual C++ and ensures the program runs smoothly</li>
  <li><b>MySQL</b> - for storing data into databases</li>
  <li><b>HeidiSQL</b> - interface for accessing MySQL</li>
</ul>

---

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

---

<h3>🎫 osTicket Installation Steps</h3>
<p>For this section, I downloaded a zip file that contains all the required installation files and then simply extracted the folder onto the desktop. The installation zip can be found <a href="https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD" target="_blank">here</a>.</p>

<details>
  <summary>⚙️ Install / Enable Internet Information Services (IIS) with CGI</summary>
  <p>To enable IIS, navigate to `Control Panel` -> `Programs` -> `Programs and Features`. Then click `Turn windows features on or off`.</p>
  <img src="https://github.com/user-attachments/assets/cc6e340c-cc45-429f-9cc0-ed4709f51623" alt="IIS Setup"/>
  <p>Select `Internet Information Services` then expand it and navigate to `World Wide Web Services` -> `Application Development Features` and check `CGI`. Then click `OK`. When the installation completes, click `Close`.</p>
  <img src="https://github.com/user-attachments/assets/03eb17c6-727b-4b31-83a0-636b65e0c3e8" alt="CGI Setup"/>
</details>

<details>
  <summary>⚙️ Install PHP for IIS</summary>
  <p>I'll need to install PHP for IIS so osTicket can run correctly. To do this, I'll navigate to the <a href="https://windows.php.net/download" target="_blank">PHP downloads page</a> and download the latest PHP version compatible with IIS (usually the "Non Thread Safe" version).</p>
  <img src="https://github.com/user-attachments/assets/4a517a4d-24db-4a0f-9394-aba34a870404" alt="Downloading PHP for IIS"/>
  <p>Once downloaded, I'll extract the contents to a folder, e.g., `C:\PHP`. Then, I need to configure IIS to recognize PHP.</p>
  <p>To do this, I open IIS Manager, click `Server`, then select `Handler Mappings`. On the right, click `Add Module Mapping`. I'll set the Request Path to `*.php`, the Module to `FastCgiModule`, and the Executable to the PHP executable file, e.g., `C:\PHP\php-cgi.exe`.</p>
  <img src="https://github.com/user-attachments/assets/a3b67c44-f8ed-451f-8cf2-c831989b15fa" alt="IIS PHP Configuration"/>
  <p>I'll also configure the `php.ini` file. To do this, I need to copy `php.ini-development` to `php.ini` and adjust necessary settings such as `upload_max_filesize` and `post_max_size` to suit the needs of osTicket.</p>
  <p>Once the configuration is complete, I'll restart IIS and test PHP by creating a file called `info.php` with the following content:</p>
  <pre>
    <?php
    phpinfo();
    ?>
  </pre>
  <p>I'll then navigate to `http://localhost/info.php` to verify if PHP is working.</p>
  <img src="https://github.com/user-attachments/assets/46717d98-b01c-49c0-b443-11b24beff8ab" alt="Testing PHP Installation"/>
</details>

<details>
  <summary>⚙️ Install MySQL</summary>
  <p>Next, I'll install MySQL to manage the database for osTicket. To do this, I'll navigate to the <a href="https://dev.mysql.com/downloads/installer/" target="_blank">MySQL Installer page</a> and download the installer.</p>
  <img src="https://github.com/user-attachments/assets/1b3d2786-149d-45a5-b2b1-bcd9b15c712b" alt="Downloading MySQL Installer"/>
  <p>After downloading, I'll run the installer and choose the `Server Only` option. I'll follow the installation wizard's prompts, setting up a root password when asked. After the installation is complete, I'll finish the setup process and start the MySQL service.</p>
  <p>To ensure MySQL is running, I'll open the `MySQL Command Line Client` and log in with the root password.</p>
  <img src="https://github.com/user-attachments/assets/0e5a279b-d0c7-4111-90fc-40fef702e4d6" alt="MySQL Command Line Client"/>
  <p>Once MySQL is set up, I'll need to create a database for osTicket. In the MySQL prompt, I'll run the following commands:</p>
  <pre>
    CREATE DATABASE osticket;
    CREATE USER 'osticket_user'@'localhost' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON osticket.* TO 'osticket_user'@'localhost';
    FLUSH PRIVILEGES;
  </pre>
  <p>This will create the `osticket` database and a user with full access to it.</p>
</details>

<details>
  <summary>⚙️ Configure osTicket</summary>
  <p>Now, I’ll configure osTicket. I’ll begin by extracting the osTicket zip file into the folder `C:\inetpub\wwwroot` on the virtual machine.</p>
  <img src="https://github.com/user-attachments/assets/dc7e6a5f-6bbd-41c6-b7a0-d88136501b22" alt="Extracting osTicket Files"/>
  <p>Then, I’ll navigate to `http://localhost` in my browser, which will trigger the osTicket installer.</p>
  <img src="https://github.com/user-attachments/assets/ea3b3da0-f357-4ed9-8e04-b0a65b2f0197" alt="Starting osTicket Installer"/>
  <p>During the installation, I’ll input the necessary database information, including the `MySQL` database name (`osticket`), the username (`osticket_user`), and the password I set earlier. The installer will verify the connection and proceed to the next step.</p>
  <img src="https://github.com/user-attachments/assets/cbe81ef8-1494-48b7-90be-6ac5e50b8a78" alt="Configuring osTicket Database"/>
  <p>Next, I'll configure the mail settings. I’ll need to set up email addresses for osTicket to handle incoming and outgoing messages. I can either use my existing SMTP server or configure a new one for this purpose.</p>
  <img src="https://github.com/user-attachments/assets/3854ebba-e7b9-4b8f-bc68-e375f23d727b" alt="Email Configuration"/>
</details>

<details>
  <summary>⚙️ Finalize osTicket Installation</summary>
  <p>Once the configuration steps are complete, I’ll click `Finish` to complete the installation process.</p>
  <img src="https://github.com/user-attachments/assets/7432f78e-b9b0-45d2-835f-d0b8e44f46e3" alt="Finishing Installation"/>
  <p>At this point, osTicket should be fully installed, and I can log into the admin panel using the username and password I set during the installation process.</p>
  <img src="https://github.com/user-attachments/assets/c2833b19-9c07-4421-bf0f-8a01d0a69a5a" alt="osTicket Admin Panel"/>
</details>

---

<h3>🎉 Completion and Next Steps</h3>
<p>Now that osTicket is up and running, I can start configuring the helpdesk system to suit my needs. From here, I can:</p>
<ul>
  <li>Set up ticket categories, SLA (Service Level Agreements), and priority levels</li>
  <li>Create user roles, including agents, administrators, and end-users</li>
  <li>Configure email notifications for ticket updates and other important alerts</li>
  <li>Integrate other systems or tools as needed</li>
</ul>
<p>In the future, I plan to experiment with additional customizations, such as integrating osTicket with a knowledge base or automating ticket workflows.</p>

<h3>➡️ Continue to My Next Project</h3>
<p>To continue with my next project, check out the <a href="https://github.com/steveabner/post-install-config" target="_blank">Post Install Configuration</a> repository on GitHub.</p>

