The certificate is probably self-signed, so you need to install it to trust it.

**Obtain the Certificate that signed the App**

If this is your own app, you should be able to find it in your IDE ( e.g. Visual Studio) otherwise use these steps:

1. Right click on APPX file
2. Click Properties
3. Click Digital Signatures
4. Select Signature from the list
5. Click Details
6. Click View Certificate
7. Click Install Certificate

**Install the Certificate**

Quote from [Installing developer packages on Windows RT](http://msdn.microsoft.com/en-us/library/windows/apps/bg126232.aspx):

> 1. From the Windows RT PC, either map the network share or connect the USB drive where you can access the AppPackages folder that contains the app package to install. Use Windows Explorer to open that folder.
> 2. Double-tap the **certificate file** in the folder and then tap **Install Certificate**. This displays the **Certificate Import Wizard**.
> 3. In the **Store Location** group, tap the radio button to change the selected option to **Local Machine**.
> 4. Click **Next**. Tap **OK** to confirm the UAC dialog.
> 5. In the next screen of the **Certificate Import Wizard**, change the selected option to **Place all certificates in the following store**.
> 6. Tap the **Browse** button. In the **Select Certificate Store** pop-up window, scroll down and select **Trusted People**, and then tap **OK**.
> 7. Tap the **Next** button; a new screen appears. Tap the **Finish** button.
> 8. A **confirmation dialog** should appear; if so, click **OK**. (If a different dialog indicates that there is some problem with the certificate, you may need to do some certificate troubleshooting. However, describing what to do in that case is beyond the scope of this topic.)