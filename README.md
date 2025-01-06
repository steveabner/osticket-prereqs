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

  ![2025-01-06 11_27_08-Window](https://github.com/user-attachments/assets/7e393428-fa95-46bf-a718-bf5b59a4c173)

- And finally, click `Create` again.

  ![2025-01-06 11_29_05-Window](https://github.com/user-attachments/assets/fe104b1a-48d7-491a-8590-4e160e6d55d6)

- The Resource Group has been created. In the next section, I will set up the virtual machine.

</details>

<details>
  <summary>💻 Creating the Virtual Machine</summary>

- On the Azure Portal, I'll search for `Virtual Machines`.

  ![2025-01-06 11_58_58-Window](https://github.com/user-attachments/assets/7b49b5b6-0448-48ad-9a98-740b48903939)

- On the Virtual Machine page, I'll click `Create` and select `Azure Virtual Machine` on the top-left.

  ![2025-01-06 12_01_45-Window](https://github.com/user-attachments/assets/62e95754-35bc-4334-ab1b-651e15280ebd)

- On the create page, I'll select the Resource Group that I just created `rg-osticket` and name the VM `osticket-vm`.

  ![2025-01-06 12_06_24-Window](https://github.com/user-attachments/assets/ae2eb56f-68f8-47bc-83ca-92dad2c922fe)

- I'll select `Windows 10 Pro (22H2)` as the image.

  ![2025-01-06 12_09_44-Window](https://github.com/user-attachments/assets/5feef9a2-d693-4c2e-9dc9-8e02fc450eb1)

- Then I'll select `Standard_D2s_v4 - 2vcpus, 8 GiB memory` as the VM size

  ![2025-01-06 12_11_35-Window](https://github.com/user-attachments/assets/0425cced-59c7-4604-a743-b7d2526b8e1e)

- Enter an Administrator username and password, agree to the licensing terms, and leave all other settings, such as disk, network, and others, at their default values. Click Review + Create, then click Create.

![2025-01-06 12_16_13-Window](https://github.com/user-attachments/assets/b3c8c8b5-fd4d-40b9-8d3b-bf2641681533)


</details>

