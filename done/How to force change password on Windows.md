#how-to , #windows , #password

Sometimes we need to use weak password for testing machine.

However, Windows restricts strong passwords based on security policy considerations.

How to do it, let we get started it.

### Prerequisites

1.  OS for Windows
2.  gpedif.msc, you must know that some windows version do not have this tool

### How to force change password on Windows

1.  Open the **run** command, and type **gpedit.msc**, then click **OK** to open the Local Group Policy Editor.
2.  Browse the following path : Computer Configuration > Windows Settings > Security Settings > Account Policies > Password Policy
3.  Look at right side, double-click the **Password must meet complexity requiremnts** policy. Then disable it, and click **OK.**
4.  Click **Sign-in** options at left side, click the button for **Change** at right side to change your machine password. 
5.  Click **Sign-in** options at left side, click the button for **Change** at right side. 
6.  Change your machine password, step by step.
7.  Finish. Logout your account, and login your account again using the new password

### Step by step

1.  Open the **run** command, and type **gpedit.msc**, then click **OK** to open the Local Group Policy Editor. 
![|300](../../attachments/How%20to%20force%20change%20password%20on%20Windows.png)
2.  Browse the following path : Computer Configuration > Windows Settings > Security Settings > Account Policies > Password Policy 
![|300](../../attachments/How%20to%20force%20change%20password%20on%20Windows-1.png)
3.  Look at right side, double-click the **Password must meet complexity requiremnts** policy. Then disable it, and click **OK.** 
![|300](../../attachments/How%20to%20force%20change%20password%20on%20Windows-2.png)
4.  Click the icon for Windows, click **Change account settings** to open settings.
![|300](../../attachments/How%20to%20force%20change%20password%20on%20Windows-3.png)
5.  Click **Sign-in** options at left side, click the button for **Change** at right side.
![|300](../../attachments/How%20to%20force%20change%20password%20on%20Windows-4.png)
6.  Change your machine password, step by step.
![|300](../../attachments/How%20to%20force%20change%20password%20on%20Windows-5.png)
![|300](../../attachments/How%20to%20force%20change%20password%20on%20Windows-6.png)
![|300](../../attachments/How%20to%20force%20change%20password%20on%20Windows-7.png)
7.  Finish. Logout your account, and login your account again using the new password

  

### Reference article

> [https://www.windowscentral.com/how-force-users-change-their-password-periodically-windows-10](https://www.windowscentral.com/how-force-users-change-their-password-periodically-windows-10)