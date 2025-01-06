<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h2>osTicket - Prerequisites and Installation</h2>
This project involves configuring all the prerequisites and installing osTicket. The setup was completed on a Windows 10 Virtual Machine that I created in Azure. You can find the installation files used in this project <a href=https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD>here</a>

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
  <summary>📦 Creating the Resource Group </summary>

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
  <summary>💻 Creating the Virtual Machine</summary>

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
  <summary>💻 Connect to the VM via RDP</summary>

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
  <summary>⚙️ Install / Enable Internet Information Services (IIS) with CGI</summary>

- To enable IIS, navigate to `Control Panel` -> `Programs` -> `Programs and Features`. Then click `Turn windows features on or off`

  ![2025-01-06 13_24_23-Window](https://github.com/user-attachments/assets/cc6e340c-cc45-429f-9cc0-ed4709f51623)

- Select `Internet Information Services` then expand it and navigate to `World Wide Web Services` -> `Application Development Features` and check `CGI`. Then click `OK`. When the installation completes, click `Close`

  ![2025-01-06 13_33_08-Window](https://github.com/user-attachments/assets/03eb17c6-727b-4b31-83a0-636b65e0c3e8)

</details>

<details>
  <summary>⚙️ Install PHP Manager & Rewrite Module</summary>

- Within the installation folder, I'll install PHPManger. `PHPManagerForIIS_V1.5.0`

  ![2025-01-06 13_46_32-Window](https://github.com/user-attachments/assets/beec8a99-f728-4f74-855d-6532c91c28b5)
  ![2025-01-06 13_46_54-Window](https://github.com/user-attachments/assets/43a4f112-9bf8-46fe-b4ff-fdde1c5b76b2)

- Then I'll install the Rewrite Module. `rewrite_amd64_en-US`
  
  ![2025-01-06 13_54_33-Window](https://github.com/user-attachments/assets/b9440967-634d-44e4-b818-c4ddafe5315e)
  ![2025-01-06 13_59_22-Window](https://github.com/user-attachments/assets/08234180-4022-48ba-aac7-f2e70a5ecdfb)

</details>

<Details>
  <Summary>📁 Create the directory C:\PHP</Summary>

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
  <summary>⚙️ Install Microsoft Visual C++ Redistibutable</summary>

- Within the installation folder, I'll open `VC_redist.x86`

  ![2025-01-06 14_34_00-Window](https://github.com/user-attachments/assets/c8ec1459-103f-453f-be8e-e652df7e5af3)

- Click `I Agree` then `Install`

  ![2025-01-06 14_34_29-Window](https://github.com/user-attachments/assets/26f9fb45-7eb2-45a5-87ef-bb48a86407ab)

</details>

<details>
  <summary>⚙️ Install MySQL</summary>

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

- When the installation wizard appears, click `Next`, then choose `Stand Configuration`, then click `Next`

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
  <summary>⚙️ Configure PHP</summary>

### Open IIS as Admin

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
