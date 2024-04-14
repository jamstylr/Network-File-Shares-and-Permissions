<p align="center">
  <img src=https://github.com/jamstylr/Network-File-Shares-and-Permissions/assets/159660523/d3f2745c-1237-4b22-91b7-5f1852398133/>
</p>


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)

<h2>File Permissions Configuration Steps</h2>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
In this lab, we'll set up shared network files and configure permissions accordingly. We'll create folders on the C:\ drive of the DC-1 VM and distribute them across the network, assigning specific permissions to individual files. Access to certain files will be restricted to designated individuals. First, we will create 4 folders located in the C:\ drive on DC-1. We'll then share these folders across the network to grant Client-1 access to them.
</p>
<br />

<p>
To share a folder and allocate permissions, access the folder's Properties and select "Share" within the "Sharing" tab. From there, you can designate network users to share with and allocate suitable permissions. Create the 4 following folders and permissions: “read-access”: should be shared with Domain Users and set Permissions to Read. “write-access”: should be shared with Domain Users and set Permissions to Read/Write. “no-access”: should be shared with Domain Admins and set Permissions to Read\Write. “accounting”: create the folder but skip share/permissions for now.
</p>
<br />

<p>
Login to Client-1 VM as a normal user and navigate to the shared folders by opening File Explorer and entering the path: \\dc-1. You can also do this by right clicking on Start, select "Run," and type “\\dc-1”. You can create a text file inside of the “write-access” folder because the permissions are set to Read/Write. In the “read-access” folder, you'll find you can view files but not add new ones. As for the “no-access” folder, access is completely denied. These permissions are tied to the Security Groups that Domain Users belong to, along with the folder-specific permissions set for those groups.
</p>
<br />

<p>
Return to the Domain Controller VM (DC-1) and open Active Directory Users and Computers. Here, create a new Organizational Unit named “_SECURITY_GROUPS”. Right-click on it to create a new group named “ACCOUNTANTS” with GroupType set to “Security”. Afterward, revisit the “accounting” folder we set up earlier. Share this folder with the ACCOUNTANTS group and set its permissions to Read/Write.
</p>
<br />

<p>
If you go back to Client-1 VM, you will notice that the user you are logged in with still doesn’t have access to the "accounting" folder. This is because the user is not a member of the ACCOUNTANTS group. To add this user to the group, first logoff Client-1. Next, go back to DC-1 -> Active Directory Users and Computers -> _SECURITY_GROUPS -> right click on ACCOUNTANTS and open Properties -> Members -> Add -> write in the user name from Client-1 -> Check Names -> Ok -> Apply -> Ok. Now go back to Client-1 and login as the user and you should now have access to the “accounting” folder.
</p>
<br />
