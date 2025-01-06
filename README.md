<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h2>osTicket - Prerequisites and Installation</h2>
This project involves configuring all the prerequisites and installing osTicket. The setup was completed on a Windows 10 Virtual Machine that I created in Azure. You can find the installation files used in this project <a href=https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD>here</a>.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Virtual Machines
- Remote Desktop
- MySQL
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10

<h2>List of Prerequisites</h2>

- <b>PHP manager for IIS</b> - ensures PHP is correctly configured to run IIS
- <b>Rewrite module </b> - facilitates URL rewriting and redirect users to URLs
- <b>VC_redist.x86</b> (redistributable) - osTicket relies on libraries that are part of Microsoft Visual C++ and ensures the program runs smoothly
- <b>MySQL</b> - for storing data into databases
- <b>HeidiSQL</b> - interface for accessing MySQL 


## 💻 Azure Resource Group and Virtual Machine Setup

<details>
  <summary>1️⃣ 📦 Creating the Resource Group </summary>

- I'll navigate to the Azure Portal and click or search for `Resource Groups`.

  ![2025-01-06 11_20_48-Window](https://github.com/user-attachments/assets/c5d5eee0-7df2-4cf4-9a71-396e7c7ebb89)

- On the Resource Group page I'll click `Create` at the top-left.

  ![2025-01-06 11_23_38-Window](https://github.com/user-attachments/assets/8d197474-33c9-4162-ad74-392986fb3249)

- I'll select my Azure subscription and name the Resource Group `rg-osticket`, set the Region to `East US 2`, then click `Review + Create`.

  ![2025-01-06 11_27_08-Window](https://github.com/user-attachments/assets/96334a91-91c2-4102-8893-b89c0442ec91)

- And finally, click `Create` again.

  ![2025-01-06 11_29_05-Window](https://github.com/user-attachments/assets/74840e04-9959-4307-9a63-2a1ee6f5a151)

- The Resource Group has been created. In the next section, I will set up the virtual machine.

</details>

<details>
  <summary>2️⃣ 💻 Creating the Virtual Machine</summary>

- On the Azure Portal, I'll search for `Virtual Machines`.

  ![2025-01-06 11_58_58-Window](https://github.com/user-attachments/assets/7b49b5b6-0448-48ad-9a98-740b48903939)

- On the Virtual Machine page, I'll click `Create` on the top-left, then select `Azure Virtual Machine`.

  ![2025-01-06 12_01_45-Window](https://github.com/user-attachments/assets/62e95754-35bc-4334-ab1b-651e15280ebd)

- On the create page, I'll select the Resource Group that I just created `rg-osticket`, and name the VM `osticket-vm`.

  ![2025-01-06 12_06_24-Window](https://github.com/user-attachments/assets/ae2eb56f-68f8-47bc-83ca-92dad2c922fe)

- I'll select `Windows 10 Pro (22H2)` as the image.

  ![2025-01-06 12_09_44-Window](https://github.com/user-attachments/assets/5feef9a2-d693-4c2e-9dc9-8e02fc450eb1)

- Then I'll select `Standard_D2s_v4 - 2vcpus, 8 GiB memory` as the VM size.

  ![2025-01-06 12_11_35-Window](https://github.com/user-attachments/assets/0425cced-59c7-4604-a743-b7d2526b8e1e)

- Enter a username and password, agree to the licensing terms, and leave all other settings, such as disk, network, and others, at their default values. Click `Review + Create`, then click `Create`.

  ![2025-01-06 12_16_13-Window](https://github.com/user-attachments/assets/b3c8c8b5-fd4d-40b9-8d3b-bf2641681533)

- The VM has been created.

  ![2025-01-06 12_26_01-Window](https://github.com/user-attachments/assets/a14f14e0-09e8-47dc-a43b-1b3aeee4de06)

</details>

<details>
  <summary>3️⃣ 💻 Connect to the VM via RDP</summary>

- Now that the VM has been created, I'll connect to it using RDP. To do this, I need the Public IP Address. In the Azure Portal, navigate to Virtual Machines, select `osticket-vm`, and copy the Public IP Address.

  ![2025-01-06 12_47_24-Window](https://github.com/user-attachments/assets/0acc73fc-c07d-412f-a6ad-708f9902ab3a)

- On my Host Machine, I'll click `Start` and type `Remote Desktop`, then click `Remote Desktop Connection`.

 - I'll click `Show Options`, input the IP Address and username, then click `Connect`.

  ![2025-01-06 12_56_43-Window](https://github.com/user-attachments/assets/4999dad2-8aee-4acb-867d-769651b2696e)

- Input the password and click `OK`

  ![2025-01-06 12_58_55-Window](https://github.com/user-attachments/assets/1042ae72-10b6-43e7-b60e-af909c1fb8e2)

- Click `Yes` to trust the certificate.

  ![2025-01-06 12_59_17-Window](https://github.com/user-attachments/assets/c66072ec-cea3-4d64-aed9-45d87627e9cd)

- I'm now logged into the VM

  ![2025-01-06 13_02_47-Window](https://github.com/user-attachments/assets/f1eeecb0-1463-424c-99fd-918f923e5895)

</details>

## 🎫 osTicket Installation Steps
For this section, I downloaded a zip file that contains all the required installation files and then simply extracted the folder onto the desktop. The installation zip can be found <a href="https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD" target="_blank">here</a>.

<details>
  <summary>1️⃣ ⚙️ Install / Enable Internet Information Services (IIS) with CGI</summary>

- To enable IIS, navigate to `Control Panel` -> `Programs` -> `Programs and Features`. Then click `Turn windows features on or off`

  ![2025-01-06 13_24_23-Window](https://github.com/user-attachments/assets/cc6e340c-cc45-429f-9cc0-ed4709f51623)

- Select `Internet Information Services` then expand it and navigate to `World Wide Web Services` -> `Application Development Features` and check `CGI`. Then click `OK`. When the installation completes, click `Close`

  ![2025-01-06 13_33_08-Window](https://github.com/user-attachments/assets/03eb17c6-727b-4b31-83a0-636b65e0c3e8)

</details>

<details>
  <summary>2️⃣ ⚙️ Install PHP Manager & Rewrite Module</summary>

- Within the installation folder, I'll install PHPManger. `PHPManagerForIIS_V1.5.0`

  ![2025-01-06 13_46_32-Window](https://github.com/user-attachments/assets/beec8a99-f728-4f74-855d-6532c91c28b5)
  ![2025-01-06 13_46_54-Window](https://github.com/user-attachments/assets/43a4f112-9bf8-46fe-b4ff-fdde1c5b76b2)

- Then I'll install the Rewrite Module. `rewrite_amd64_en-US`
  
  ![2025-01-06 13_54_33-Window](https://github.com/user-attachments/assets/b9440967-634d-44e4-b818-c4ddafe5315e)
  ![2025-01-06 13_59_22-Window](https://github.com/user-attachments/assets/08234180-4022-48ba-aac7-f2e70a5ecdfb)

</details>

<Details>
  <Summary>3️⃣ 📁 Create the directory C:\PHP</Summary>

- Open File Explorer, click `This PC`, then open `C drive`

  ![2025-01-06 14_09_29-Window](https://github.com/user-attachments/assets/785f1ad6-7931-46ce-b026-526921761006)

- In the C drive, right-click, go to `New`, and then select `Folder`

  ![2025-01-06 14_11_11-Window](https://github.com/user-attachments/assets/b280dd59-00fc-4ddf-8388-e1f0bbb56e99)

- Name the folder `PHP`

  ![2025-01-06 14_14_06-Window](https://github.com/user-attachments/assets/d1eeb1aa-5391-4d4a-84d2-6853a14754ea)

- Within the installation folder, I'll right-click the `php-7.3.8-nts-Win32-VC15-x86` folder, then select `Extract All`. I'll set the destination folder to `C:\PHP` then click `Extract`

  ![2025-01-06 14_19_45-Window](https://github.com/user-attachments/assets/23f3e116-faf3-41df-944b-8e3ded955bdd)
  ![2025-01-06 14_22_18-Window](https://github.com/user-attachments/assets/90998ab4-b60a-47c6-aa60-81588fa2ff13)

</Details>

<details>
  <summary>4️⃣ ⚙️ Install Microsoft Visual C++ Redistibutable</summary>

- Within the installation folder, I'll open `VC_redist.x86`

  ![2025-01-06 14_34_00-Window](https://github.com/user-attachments/assets/c8ec1459-103f-453f-be8e-e652df7e5af3)

- Click `I Agree` then `Install`

  ![2025-01-06 14_34_29-Window](https://github.com/user-attachments/assets/26f9fb45-7eb2-45a5-87ef-bb48a86407ab)

</details>

<details>
  <summary>5️⃣ ⚙️ Install MySQL</summary>

- Within the installation folder, I'll open `mysql-5.5.62-win32`

  ![2025-01-06 14_43_12-Window](https://github.com/user-attachments/assets/b44b6d54-d974-4e0c-9066-e9f9bf3d05ab)

- Click `Next`, then check `I accept`, then click `Next` again.

  ![2025-01-06 14_44_02-Window](https://github.com/user-attachments/assets/a80b0304-82d2-420e-a83a-890bd8b42f72)
  ![2025-01-06 14_44_18-Window](https://github.com/user-attachments/assets/b528ef12-431a-4bae-a044-7032a60c2f47)

- Choose `Typical` then click `Install`

  ![2025-01-06 14_46_14-Window](https://github.com/user-attachments/assets/81d713cb-19dd-4958-8e4e-956fdd5d4644)
  ![2025-01-06 14_46_26-Window](https://github.com/user-attachments/assets/e621a60d-18be-439a-ba92-1417531c0c3b)

- I'll choose to launch the configuration wizard, click `Finish`

  ![2025-01-06 14_47_24-Window](https://github.com/user-attachments/assets/37361e27-0403-40ea-aa9f-fe0359b9a0bc)

- When the installation wizard opens, click `Next`, then choose `Stand Configuration`, then click `Next`

  ![2025-01-06 14_49_17-Window](https://github.com/user-attachments/assets/2a6f5fdf-ace6-4698-8ceb-ed7916ace04f)
  ![2025-01-06 14_49_32-Window](https://github.com/user-attachments/assets/e8611aa6-626e-41f3-97aa-5c9e7e38b8fa)

- On the next window, I'll leave everything as is, and click `Next`

  ![2025-01-06 14_51_31-Window](https://github.com/user-attachments/assets/7d58a234-df62-40b7-9254-1ca066238c9d)

- Input a password, then click `Next`

  ![2025-01-06 14_53_48-Window](https://github.com/user-attachments/assets/cde5b353-c912-49f8-8838-a8f60a243ff2)

- Click `Execute`, once it's complete, click `Finish`.

  ![2025-01-06 14_55_38-Window](https://github.com/user-attachments/assets/72255ef1-6922-4158-bec4-630fbe1dd0f7)
  ![2025-01-06 14_56_14-Window](https://github.com/user-attachments/assets/60ba0419-10af-4600-ad6c-6c6e6528ed91)


</details>

<details>
  <summary>6️⃣ ⚙️ Configure PHP</summary>

### Open IIS and run as Administrator

- Click start, then type `IIS`, right click `Internet Information Services (IIS)`, then select `Run as administrator`

  ![2025-01-06 15_40_56-Window](https://github.com/user-attachments/assets/7d48542f-50d3-411a-a918-8215892e52b5)

### Register PHP from within IIS

- Within IIS, open `PHP Manger`

  ![2025-01-06 15_44_17-Window](https://github.com/user-attachments/assets/87e9cdf4-f5fe-476b-ad7b-cd59b10b1ec8)

- In PHP Manager, click `Register new PHP version`

  ![2025-01-06 15_45_39-Window](https://github.com/user-attachments/assets/d4130330-8070-4c89-bdfc-9dc9b6c236f6)

- Browse to `C:\PHP\php-cgi.exe`, then click `OK`

  ![2025-01-06 15_47_49-Window](https://github.com/user-attachments/assets/0e551cb6-1bc0-4236-87d5-975aed3eaaf4)
  ![2025-01-06 15_48_06-Window](https://github.com/user-attachments/assets/88558984-c733-49a8-bf90-4ed0979af190)

- Reload IIS by right-clicking `osticket-vm` on the top-left and selecting `Stop`, then right-click again and select `Start`

  ![2025-01-06 15_51_12-Window](https://github.com/user-attachments/assets/79d3328b-2c42-4a29-b63f-352ceee690c7)
  ![2025-01-06 15_50_49-Window](https://github.com/user-attachments/assets/d16cf2a8-273e-4b9a-abd1-fdb39d807838)

</details>

<details>
  <summary>7️⃣ ⚙️ Install HeidiSQL</summary>

- Within the installation folder, I'll open `HeidiSQL_12.3.0.6589_Setup`.

  ![2025-01-06 17_12_39-Window](https://github.com/user-attachments/assets/a6503e62-731b-4b87-862a-199c93fcb382)

- Click `I Accept`, then click `Next`.

  ![2025-01-06 17_13_54-Window](https://github.com/user-attachments/assets/18f1feb3-4e66-4222-9bbd-90cdcb9f16c8)

- Click `Next`, `Next`, `Install`.

  ![2025-01-06 17_15_57-Window](https://github.com/user-attachments/assets/e45fd4c6-532e-4fa1-9927-897a54709fdc)

- Then click `Finish`.

  ![2025-01-06 17_16_17-Window](https://github.com/user-attachments/assets/c3a9988c-e714-4574-9f6c-12aa68f77f97)

- Open HeidiSQL, then click `Skip`.

  ![2025-01-06 17_18_21-Window](https://github.com/user-attachments/assets/852e7118-1870-40fe-b949-603374011510)

- Click `New` at the bottom left.

  ![2025-01-06 17_19_09-Window](https://github.com/user-attachments/assets/ab63332c-5cb4-4e9c-ac1e-d022bd75e834)

- I'll input the username and password I set up when installing MySQL, then click `Open`.

  ![2025-01-06 17_20_30-Window](https://github.com/user-attachments/assets/2b339c13-340a-40c0-98de-cb86150f8f01)

- Now I'll create a database called `osTicket`.  Right-click `Unnamed` go to `Create New`, then click `Database`, I'll name it `osTicket`, then click `OK`.

  ![2025-01-06 17_32_22-Window](https://github.com/user-attachments/assets/c77380fe-38ab-4985-9e75-981d78be699f)
  ![2025-01-06 17_33_42-Window](https://github.com/user-attachments/assets/a4e053a9-5f36-46af-ac9d-07c8e91a740c)
  
- The osTicket database has been created.

  ![2025-01-06 17_34_41-Window](https://github.com/user-attachments/assets/13390e02-1855-46d0-a900-27f93d688802)

</details>

<details>
  <summary>8️⃣ ⚙️ Install osTicket</summary>

- Within the installation folder, I'll extract `osTicket-v1.15.8`, then open the folder.

  ![2025-01-06 16_04_12-Window](https://github.com/user-attachments/assets/20360c1f-74e0-4a2c-9390-48de67a2a96c)
  ![2025-01-06 16_07_02-Window](https://github.com/user-attachments/assets/69fc5dc5-9a03-4990-98e5-3d4841d6fd71)

- In a separate window, I'll navigate to `C:\inetpub\wwwroot`

  ![2025-01-06 16_08_21-Window](https://github.com/user-attachments/assets/13538105-3420-45a0-8d03-1e1e9d31a87a)

- From here, I need to copy the `upload` folder into the `wwwroot` folder.

  ![2025-01-06 16_11_16-Window](https://github.com/user-attachments/assets/f4c6fb67-945d-4fc4-8525-6e4aee8d2ecc)

- Now I'll rename the `upload` folder to `osTicket`

  ![2025-01-06 16_12_17-Window](https://github.com/user-attachments/assets/b969b9e2-8694-4422-9d54-446a56e050d9)

- Now I'll reload the IIS server by right-clicking `osticket-vm` on the top-left and selecting `Stop`, then right-click again and selecting `Start`

  ![2025-01-06 15_51_12-Window](https://github.com/user-attachments/assets/79d3328b-2c42-4a29-b63f-352ceee690c7)
  ![2025-01-06 15_50_49-Window](https://github.com/user-attachments/assets/d16cf2a8-273e-4b9a-abd1-fdb39d807838)

### Confirm the osTicket Site loads

- Within the IIS Manager, I'll expand `osticket-vm` -> `Sites` -> `Default Web Site`. Click `osTicket` then click `Browse *:80 (HTTP)` in the right pane.

  ![2025-01-06 16_22_01-Window](https://github.com/user-attachments/assets/b3a4bff3-8ab9-4d0c-ada2-36a3e292d4a7)

- The osTicket Website has loaded successfully!

  ![2025-01-06 16_23_38-Window](https://github.com/user-attachments/assets/487396d3-17a7-421f-aab9-897234d15d5b)

- Notice that some extensions are not enabled, I will do that next.

  ![2025-01-06 16_27_01-Window](https://github.com/user-attachments/assets/06259e65-09af-4aac-8047-044019d80451)

- Open IIS Manager, go to `Sites`, `Default Web Site`, `osTicket`, then open `PHP Manager`.

  ![2025-01-06 16_29_21-Window](https://github.com/user-attachments/assets/6dcdbbef-b504-4790-8039-4c3c69732ecb)

- Within PHP Manager, Click `Enable or disable an extension`

  ![2025-01-06 16_31_05-Window](https://github.com/user-attachments/assets/acb166d7-74f6-4d7b-9765-f9f9f03846de)

- I'll right-click and enable the following:
  - php_imap.dll
  - php_intl.dll
  - php_opcache.dll

  ![2025-01-06 16_34_57-Window](https://github.com/user-attachments/assets/9f098179-b46f-47ec-950c-e3b187c212ee)

### Rename ost-sampleconfig.php

- I'll browse to `C:\` -> `inetpub` -> `wwwroot` -> `osTicket` -> `include`

  ![2025-01-06 16_42_52-Window](https://github.com/user-attachments/assets/cc55a877-4947-4e8a-b885-3a5b86c24cef)

- In the `include` folder, I'll find `ost-sampleconfig.php` and rename is to `ost-config.php`

  ![2025-01-06 16_44_23-Window](https://github.com/user-attachments/assets/28ec1b47-836f-409d-83cd-d32ae1331aab)

### Give osTicket permission to access the file

- Right-click `ost-config.php` and select properties.

  ![2025-01-06 16_50_24-Window](https://github.com/user-attachments/assets/69ff9c01-c32b-4edb-8f5d-7a4b74994ba8)

- Click the `Security` tab, then click `Advanced`

  ![2025-01-06 16_51_28-Window](https://github.com/user-attachments/assets/b1e0ccd2-b178-4a37-b150-5d1269e786d6)

- I will click `Disable inheritance`, then click `Remove all inherited permissions from this object`

  ![2025-01-06 16_53_42-Window](https://github.com/user-attachments/assets/61742b1c-6add-479a-bd9d-eac8ef9e9028)
  ![2025-01-06 16_54_36-Window](https://github.com/user-attachments/assets/19e76ab4-933c-42b9-a221-5eb7a5cb6a7e)

- Next, I'll click `Add`

  ![2025-01-06 16_56_12-Window](https://github.com/user-attachments/assets/06a5eb14-4407-4000-8129-0b8dfb57df74)

- Click `Select a principal`

  ![2025-01-06 16_57_17-Window](https://github.com/user-attachments/assets/52280ac8-2425-4a0a-81ce-67c89e1d46f0)

- I'll input `everyone`, click `Check Names`, then click `OK`

  ![2025-01-06 17_00_54-Window](https://github.com/user-attachments/assets/6e171555-58b7-4edf-9047-a689f679bb81)

- Check `Full Control`, then click `OK`

  ![2025-01-06 17_02_01-Window](https://github.com/user-attachments/assets/8eae278d-bb1f-4e2c-9a2a-f9b4308cc9d6)

- Click `Apply`, `OK`, then `OK` again.

  ![2025-01-06 17_02_48-Window](https://github.com/user-attachments/assets/ac474b5a-62b3-49fc-9080-30a5c1db1d90)

### Continue osTicket setup

- I'll go back to the osTicket website and click `Continute`

  ![2025-01-06 17_04_49-Window](https://github.com/user-attachments/assets/ed7bebfe-9605-418c-9d35-b3e11bf0b337)

- I'll fill out the information and input my usernames and password, then click `Install`

  ![2025-01-06 17_40_37-Window](https://github.com/user-attachments/assets/c7e91187-0f5b-4352-b853-4837b6e6b9f3)

- When complete, I'll get a `Congratulations!` window.

  ![2025-01-06 17_41_53-Window](https://github.com/user-attachments/assets/817dce73-867b-4e03-a843-2715948fa083)

## ✅ Installation Complete!

- This wraps up my osTicket Prerequisites and Installation project!

</details>
