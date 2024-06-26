<p align="center">
  <img src=https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/d3f2745c-1237-4b22-91b7-5f1852398133/>
</p>

<h1>Network File Shares and Permissions</h1>
This tutorial examines file permissions and shares within an Active Directory domain environment. These elements are pivotal in ensuring that users are granted appropriate permissions and access to essential files they need. This tutorial builds upon a previous lab where I set up a client connected to the domain “mydomain.com". On the Domain Controller VM, I'm logged in as mydomain.com\jane_admin. On the Client VM, I am logged in as a random user that was generated through the Powershell script in the Active Directory lab.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)

<h2>File Permissions Configuration Steps</h2>

![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/b2d3771b-9bef-424a-b08e-89726d6e5ed3)
<p>
In this lab, we'll set up shared network files and configure permissions accordingly. We'll create folders on the C:\ drive of the DC-1 VM and distribute them across the network, assigning specific permissions to individual files. Access to certain files will be restricted to designated individuals. First, we will create 4 folders located in the C:\ drive on DC-1. The 4 folders will be named: "read-access", "write-access", "no-access", and "accounting". We'll then share these folders across the network to grant Client-1 access to them.
</p>
<br />

![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/a0fcf52e-e45c-4f48-b14d-560d0dd098fc)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/ad201111-13f3-4fa6-a65d-46791f6ac19a)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/6fa67eb5-ef68-4a01-82ef-180fbe97d970)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/4cacffc3-7546-48a2-8eab-a34d10ce82e3)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/c8948666-04d7-49ad-92cf-6c7e13d80699)

<p>
To share a folder and allocate permissions, access the folder's Properties and select "Share" within the "Sharing" tab. From there, you can designate network users to share with and allocate suitable permissions. Create the 4 following folders and permissions: “read-access”: should be shared with Domain Users and set Permissions to Read. “write-access”: should be shared with Domain Users and set Permissions to Read/Write. “no-access”: should be shared with Domain Admins and set Permissions to Read\Write. “accounting”: create the folder but skip share/permissions for now.
</p>
<br />

![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/60514ab2-84ee-44b9-8800-f775d488934f)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/e4866a8c-1da5-400c-8d2e-142f38d5a596)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/f71cd233-6b74-4fed-a3cb-dac0727f1c72)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/b6c17e07-a667-4743-9d06-7fa0af5ab4bb)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/7a36fe7e-cdb4-4936-8d49-b64dc8c84120)
<p>
Login to Client-1 VM as a normal user and navigate to the shared folders by opening File Explorer and entering the path: \\dc-1. You can also do this by right clicking on Start, select "Run," and type “\\dc-1”. You can create a text file inside of the “write-access” folder because the permissions are set to Read/Write. In the “read-access” folder, you'll find you can view files but not add new ones. As for the “no-access” folder, access is completely denied. These permissions are tied to the Security Groups that Domain Users belong to, along with the folder-specific permissions set for those groups.
</p>
<br />

![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/900483f4-1e1f-4de9-92a5-6d6bac350836)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/43bdb5c9-b092-46fa-8559-c8d595b86b3a)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/47ac8932-a09e-461c-bbb8-44031169b9bf)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/d3e4aecf-84b7-4b7a-bc05-a8360c647b9c)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/f635b6ed-aee0-47a2-81a6-95614f3d8d67)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/3886c1da-95ea-44dc-b608-be14be16d51f)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/703a8e05-98b5-474e-8bb1-bfd4585481f8)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/58f67bce-3cb9-4e07-8d5f-9d378a4fb6a4)
<p>
Return to the Domain Controller VM (DC-1) and open Active Directory Users and Computers. Here, create a new Organizational Unit named “_SECURITY_GROUPS”. Right-click on it to create a new group named “ACCOUNTANTS” with GroupType set to “Security”. Afterward, revisit the “accounting” folder we set up earlier. Share this folder with the ACCOUNTANTS group and set its permissions to Read/Write.
</p>
<br />

![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/05eb1faa-3479-4c6c-9f62-a0b44591b194)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/eee26088-e13a-405d-812d-8f6f1dad1aab)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/d2cfb954-1855-4718-839b-b5f5c9d02563)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/6af8f1f4-ae77-4e0d-a8d6-1595771e43ea)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/91b58a59-545d-44ff-bec5-45d9de81b2a4)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/93fbaa0e-a81a-4ce6-8345-077fe4a4d082)
![image](https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/bcdac863-ff45-4ec3-bb3c-7a147c637fe5)
<p>
If you go back to Client-1 VM, you will notice that the user you are logged in with still doesn’t have access to the "accounting" folder. This is because the user is not a member of the ACCOUNTANTS group. To add this user to the group, first logoff Client-1. Next, go back to DC-1 -> Active Directory Users and Computers -> _SECURITY_GROUPS -> right click on ACCOUNTANTS and open Properties -> Members -> Add -> write in the user name from Client-1 -> Check Names -> Ok -> Apply -> Ok. Now go back to Client-1 and login as the user and you should now have access to the “accounting” folder.
</p>
<br />
