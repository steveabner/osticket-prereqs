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


## ☁️💻 Azure Resource Group and Virtual Machine Setup

<details>
  <summary>💻 Creating a Resource Group and Virtual Machine </summary>

- I'll navigate to the Azure Portal and click or search for `Resource Groups`

  ![2025-01-06 11_20_48-Window](https://github.com/user-attachments/assets/c5d5eee0-7df2-4cf4-9a71-396e7c7ebb89)

- On the Resource Group page I'll click `Create` at the top-left.

  ![2025-01-06 11_23_38-Window](https://github.com/user-attachments/assets/8d197474-33c9-4162-ad74-392986fb3249)

- I'll select my Azure subscription and name the Resource Group `rg-osticket`, set the Region to `East US 2`, then click `Review + Create`

  ![2025-01-06 11_27_08-Window](https://github.com/user-attachments/assets/7e393428-fa95-46bf-a718-bf5b59a4c173)

- And finally, click `Create` again.

  ![2025-01-06 11_29_05-Window](https://github.com/user-attachments/assets/fe104b1a-48d7-491a-8590-4e160e6d55d6)

- 



  
</details>
