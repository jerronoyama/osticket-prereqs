<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Microsoft Azure account
- Windows 10 Virtual Machine (4 vCPUs recommended)
- Remote Desktop client (RDP)
- osTicket-Installation-Files.zip package
- Internet connection inside the VM
- Administrative rights on the VM


## Installation Steps

### 1. Create Azure VM
- Create a Windows 10 VM named `osticket-vm`
- Use recommended size: 4 vCPUs
- Set username: `labuser`
- Connect via Remote Desktop

<img width="1792" height="1120" alt="image" src="https://github.com/user-attachments/assets/801702e4-d843-44d5-8a32-1667b42f1349" />


### 2. Download & Extract osTicket Files
- Download `osTicket-Installation-Files.zip`
- Extract it to the Desktop

<img width="1792" height="1120" alt="image" src="https://github.com/user-attachments/assets/2c73491a-4156-4741-be42-9da6cd8b697e" />


### 3. Install & Enable IIS with CGI
- Open "Turn Windows features on or off"
- Enable:
  - Internet Information Services (IIS)
  - World Wide Web Services
  - Application Development Features → CGI

<img width="1792" height="1120" alt="Screenshot 2025-11-28 at 4 43 39 PM" src="https://github.com/user-attachments/assets/52537163-196f-4475-99c5-bc25126f2066" />


### 4. Install PHP Manager & Rewrite Module
- Install `PHPManagerForIIS_V1.5.0.msi`
- Install `rewrite_amd64_en-US.msi`

<img width="1792" height="1120" alt="image" src="https://github.com/user-attachments/assets/81cf9242-1889-4f64-b6ca-67b05d35c2a4" />

<img width="1792" height="1120" alt="image" src="https://github.com/user-attachments/assets/ae0d8859-a417-4b26-aa0a-7d6c660799fb" />


### 5. Set Up PHP
- Create folder: `C:\PHP`
- Extract PHP 7.3.8 into `C:\PHP`
- Install `VC_redist.x86.exe`

<img width="1792" height="1120" alt="image" src="https://github.com/user-attachments/assets/61f614bd-2172-4800-9c61-7070ef6d4d05" />



### 6. Install MySQL Server 5.5
- Run `mysql-5.5.62-win32.msi`
- Typical Setup
- Standard Configuration
  - Username: `root`
  - Password: `root`

<img width="1792" height="1120" alt="image" src="https://github.com/user-attachments/assets/01bd2ac2-f858-4efc-9138-f77ad6b21310" />




### 7. Register PHP in IIS
- Open IIS Manager as Administrator
- PHP Manager → Register PHP
- Select: `C:\PHP\php-cgi.exe`
- Restart IIS

📸 *Screenshot: PHP registered in IIS*


### 8. Install osTicket Application
- Extract `osTicket-v1.15.8.zip`
- Copy the **upload** folder to `C:\inetpub\wwwroot`
- Rename folder to `osTicket`
- Restart IIS

📸 *Screenshot: osTicket folder in wwwroot*


### 9. Enable Required PHP Extensions
In IIS → PHP Manager → Enable/Disable Extensions:

Enable:
- php_imap.dll
- php_intl.dll
- php_opcache.dll

📸 *Screenshot: Enabled PHP extensions in IIS*


### 10. Configure ost-config.php
- Rename:
  `ost-sampleconfig.php` → `ost-config.php`
- Modify permissions:
  - Disable inheritance
  - Give Everyone → Full Control

📸 *Screenshot: ost-config.php permissions*


### 11. Create MySQL Database (HeidiSQL)
- Open HeidiSQL
- Create new session: root/root
- Create database named `osTicket`

📸 *Screenshot: Newly created osTicket database*


### 12. Complete osTicket Setup in Browser
Visit: `http://localhost/osTicket/`

- Enter Helpdesk name
- Default email
- Database settings:
  - Database: `osTicket`
  - Username: `root`
  - Password: `root`
- Install

📸 *Screenshot: osTicket installation success page*


### 13. Post-Installation Cleanup
- Delete: `C:\inetpub\wwwroot\osTicket\setup`
- Set `ost-config.php` to Read-only

📸 *Screenshot: Read-only permissions on ost-config.php*
