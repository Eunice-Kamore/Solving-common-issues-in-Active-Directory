<h1>Overview: Lab 6 Solving Common Active Directory Issues, Use of CMD Commands and Troubleshooting an Offline PC</h1>

This section of my home lab documentation explores **Common Active Directory Issues**, troubleshooting with **CMD commands**, and resolving situations where a **PC is offline** in a domain environment. The project provides practical solutions for addressing common problems that administrators face when working with Active Directory, such as authentication failures, group policy application issues, and troubleshooting offline PCs.

<h2>Objectives</h2>

- Identify and resolve **common Active Directory issues**, such as login problems and account lockouts.
- Use **CMD commands** to troubleshoot and resolve issues related to domain connectivity, account authentication, and more.
- Handle scenarios where a **PC is offline** or has fallen off from the domain, including troubleshooting network connectivity and domain membership.
- Understand how to diagnose and repair issues using Active Directory logs, CMD commands, and networking tools.



<h2>Documentation</h2>

In this home lab, we will explore common Active Directory issues users might encounter, then use CMD commands to resolve PC offline problems.

Let's begin with some CMD commands. On the local user account **Hellena James**, open **Command Prompt** and type `ping 10.0.2.15`. This is the IP address of our **Windows Server 2022** machine. This command will confirm that **Windows 10 VM** can communicate with the server. Now, let's repeat the process on the **Server** by pinging **Windows 10 VM**, `ping 10.0.2.16` to verify the connection from the server side.




1. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/One.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 1"/>
   <br />
   <br />
</p>

Now on our Windows Server 2022, when we ping 10.0.2.16 (local user Hellena James), we can see that the connection timed out. This is because the firewall on that account is preventing the ping, so we would need to disable it. To do that, open up Windows Defender Firewall → Turn off Windows Defender Firewall off.

2. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Two.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 2"/>
   <br />
   <br />
</p>

Use the domain administrative login credentials to access Windows Defender Firewall, then turn off all of the options. Afterward, select OK to apply the changes.

3. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Three.PNG?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 3"/>
   <br />
   <br />
</p>

4. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Four.PNG?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 3"/>
   <br />
   <br />
</p> 

5. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Five.PNG?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 3"/>
   <br />
   <br />
</p>


Now lets run the command line again on our Windows Server 2022. 

6. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Six.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 4"/>
   <br />
   <br />
</p>

If we add the -t option to our ping command, such as ping 10.0.2.16 -t, it will continue running indefinitely until manually stopped. This allows us to monitor network connectivity and observe any changes in packet loss over time. 

7. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Seven.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 5"/>
   <br />
   <br />
</p>

Next, on the local user Hellena James, run Command Prompt as an administrator using the Administrative login. Then, type gpresult /r > c:\results.txt. This command will generate a group policy report for the PC and save it as a text file in the C: drive.


8. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Eight.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 6"/>
   <br />
   <br />
</p>


9. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Nine.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 7"/>
   <br />
   <br />
</p>

10. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Ten.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 7"/>
   <br />
   <br />
</p>

If we do not run it as administrator then the command line will deny us access.

11. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Eleven.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 8"/>
   <br />
   <br />
</p>

Some additional command lines such as gpupdate /help will provide a list of available options for the gpupdate command.


12. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Twelve.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 9"/>
   <br />
   <br />
</p>

Gpresult /? will display a list of available options for the command.

13. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Thirteen.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 10"/>
   <br />
   <br />
</p>

Gpresult /r  displays the result of the Group Policy for the current user and computer.

14. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Fourteen.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 11"/>
   <br />
   <br />
</p>

Next, let's explore some common issues that Helpdesk teams may encounter when assisting users, such as when a user account becomes locked out. To test this, we will sign out of Hellena James and purposely lock her account by signing in with an incorrect password. 

15. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Fifteen.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 12"/>
   <br />
   <br />
</p>

In this scenario when a user is locked out and is calling the helpdesk or the admin for help, typically they would access the Active Directory Users and Computers → search for the user then unlock it from there. Lets try this out on the server. Open up Active Directory Users and Computers  → right-click on the domain **junicetechie.com** and search up Hellena James using the find feature, make sure that the entire directory is selected. Once Hellena James is found, double click on her name and select “Account” then check the “Unlock Account” box, then press “Apply” then “OK”. Now Hellena can log into her account successfully.

16. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Sixteen.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 13"/>
   <br />
   <br />
</p>

17. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Seventeen.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 14"/>
   <br />
   <br />
</p>

18. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Eighteen.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 14"/>
   <br />
   <br />
</p>


Hellena should be able to log in now once his account is unlocked. 


19. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Ninenteen.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 14"/>
   <br />
   <br />
</p>


Now let’s create an issue where Hellena’s account is disabled for some reason and that she forgot her password. Let’s intentionally disable her account by right clicking on her account again in Active Directory Users and Computers.

20. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Twenty.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 15"/>
   <br />
   <br />
</p>


Now let’s imagine a scenario where Hellena’s account is disabled for some reason, and she does not remember her password. As a helpdesk person, we can look up Hellena's user account in Active Directory Users and Computers using the Find feature,right-click on the domain → select Find → Entire Directory and search for Hellena James → right-click on her name and select Enable Account.

21. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Twenty%20one.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 15"/>
   <br />
   <br />
</p>  


22. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Twenty%20Two.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 16"/>
   <br />
   <br />
</p>


Since Hellena has forgotten her password, we can provide her with a temporary password that will allow him to log in and change it to a new password. To do this, right-click on the user Hellena James and select Reset Password. Ensure that the "User must change password at next logon" option is enabled.

23. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Twenty%20Three.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 17"/>
   <br />
   <br />
</p>

24. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Twenty%20Four.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 18"/>
   <br />
   <br />
</p>

25. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Twenty%20Five.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 19"/>
   <br />
   <br />
</p>


Now, let’s create a scenario where **Hellena's** account is expired due to inactivity or because an administrator has set an expiration date for the account. To do this:

Find **Hellena James** account in **Active Directory Users and Computers** and double-click on the name → Click on the **Account** tab → Under **Account expires**, select **End of** and choose a date that has already passed.

26. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Twenty%20Six.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 21"/>
   <br />
   <br />
</p>


27. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Twenty%20Seven.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 22"/>
   <br />
   <br />
</p>

To resolve this, the Admin would need to go to Active Directory Users and Computers → search for Hellena James using the Find feature in the domain → select Entire Directory → open **Hellena James's** account → go to the Account tab, then select Never under Account expires.

28. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Twenty%20Eight.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 23"/>
   <br />
   <br />
</p>

To make sure Hellena's account is valid, open Command Prompt on the server and type net user hellena.james /domain. This will verify that the account is active and should allow her to log in.


29. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Twenty%20Nine.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 24"/>
   <br />
   <br />
</p>

Let’s create an issue where the computer has fallen off the domain. In Active Directory Users and Computers → select Computers → right-click on the computer and select Disable Account.

30. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Thirty.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 25"/>
   <br />
   <br />
</p>

Now when we login it should give us an error.

31. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Thirty%20One.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 26"/>
   <br />
   <br />
</p>

When a computer is fallen off from a domain, we can sometimes fix it by going to Active Directory Users and Computers and selecting that computer and enabling it. We can now log in back into our domain accounts.

32. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Thirty%20Two.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 27"/>
   <br />
   <br />
</p>


Now let’s try a different way of making the computer fall off the domain. We will delete the listed computer from the domain. In **Active Directory Users and Computers** on the **Helpdesk** account, select **Computers**, then right-click on the computer and select Delete.

Next, let’s create a new user: go to **Users**, right-click, and select **New** → **User**. Use **First/Last Name** and set the **User logon** as **Test**, then click **Finish**.

Now, attempt to log in to our Windows 10 Machine using the **Test** account. An error should appear indicating that the computer is no longer part of the domain.

33. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Thirty%20twoo.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 28"/>
   <br />
   <br />
</p>

34. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Thirty%20Three.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 28"/>
   <br />
   <br />
</p>

To add the computer back into our domain, we need to log into our domain we need to login locally using an administrator or local user account. In this case we shall user the local user account that we created when we first installed Windows 10 since we had not enabled the administrator account. To do that type “.\Local User” and enter your password.

35. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Thirty%20Four.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 29"/>
   <br />
   <br />
</p>

Next, go into File Explorer → right-click on This PC → select Properties → click on Rename this PC (Advanced) → select Change → under Member of, change it to Workgroup. Then, restart the computer.


36. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Thirty%20Five.PNG?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 30"/>
   <br />
   <br />
</p>

Log in as **Local User** and repeat the process to add the computer back to the domain. Go to **File Explorer** → right-click on **This PC** → select **Properties** → click on **Rename this PC (Advanced)** → select **Change**, then add it back to the domain as **junicetechie.com**. Proceed with a restart.

Now, go back to **Active Directory Users and Computers**, and under **Computers**, you should see **Desktop1** is back in the domain.


37. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Thirty%20Six.PNG?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 31"/>
   <br />
   <br />
</p>

38. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Thirty%20Seven.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 31"/>
   <br />
   <br />
</p>

39. <p align="center">
   <img src="https://github.com/Eunice-Kamore/Solving-common-issues-in-Active-Directory/blob/main/Images/Thirty%20Eight.png?raw=true" height="100%" width="100%" alt="Disk Sanitization Steps 31"/>
   <br />
   <br />
</p>

Congratulations! We have successfully addressed several common Active Directory issues, utilized CMD commands effectively, and resolved PC offline scenarios. 

 👉 [Next Lab 7 : Security Groups, Mapped Drives, Personal Drives]
