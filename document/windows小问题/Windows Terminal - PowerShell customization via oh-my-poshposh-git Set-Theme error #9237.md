# Windows Terminal - PowerShell customization via oh-my-posh/posh-git Set-Theme error? #9237

 Closed

[nihaltowfiq](https://github.com/nihaltowfiq) opened this issue on 21 Feb · 3 comments

 Closed

# [Windows Terminal - PowerShell customization via oh-my-posh/posh-git Set-Theme error?](https://github.com/microsoft/terminal/issues/9237#)#9237

[nihaltowfiq](https://github.com/nihaltowfiq) opened this issue on 21 Feb · 3 comments

## Comments

[![@nihaltowfiq](https://avatars.githubusercontent.com/u/62647867?s=88&u=03fd57cabc333aa2e4eb49a766ef5e7be3345640&v=4)](https://github.com/nihaltowfiq)

 

### **[nihaltowfiq](https://github.com/nihaltowfiq)** commented [on 21 Feb](https://github.com/microsoft/terminal/issues/9237#issue-812868306)

Windows Terminal - PowerShell customization via oh-my-posh/posh-git Set-Theme error?I follow the exact tutorial of Microsoft link: [Link Here](https://docs.microsoft.com/en-us/windows/terminal/tutorials/powerline-setup) video link: [Video Link Here](https://www.youtube.com/watch?v=lu__oGZVT98&feature=youtu.be)I have installed Posh-Git and Oh-My-Posh: via this code - `Install-Module posh-git -Scope CurrentUser` `Install-Module oh-my-posh -Scope CurrentUser`I have installed PSReadLine: via this code - `Install-Module -Name PSReadLine -Scope CurrentUser -Force -SkipPublisherCheck`I am also created Microsoft.PowerShell_profile.ps1 file by typing- code $PROFILE, in my PowerShell profile and copy/paste this code: `Import-Module posh-git` `Import-Module oh-my-posh` `Set-Theme Paradox`But I get this error:Set-Theme Paradox The term 'Set-Theme' is not recognized as a name of a cmdlet, function, script file, or executable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.ScreenShot: [Screenshot of error](https://i.stack.imgur.com/hUy8j.png)[![ssss](https://user-images.githubusercontent.com/62647867/108628039-c2573e00-7482-11eb-9f4c-e8e13f403435.PNG)](https://user-images.githubusercontent.com/62647867/108628039-c2573e00-7482-11eb-9f4c-e8e13f403435.PNG)

👍 2

<details class="details-overlay details-reset dropdown hx_dropdown-fullscreen position-relative float-left d-inline-block reaction-popover-container reactions-menu js-reaction-popover-container" style="box-sizing: border-box; display: inline-block !important; position: relative; float: left !important;"><summary class="btn-link reaction-summary-item add-reaction-btn" aria-label="Add your reaction" aria-haspopup="menu" role="button" style="box-sizing: border-box; display: inline-block; cursor: pointer; padding: 9px 15px 7px; font-size: inherit; color: var(--color-text-link); text-decoration: none; white-space: nowrap; user-select: none; background-color: initial; border: 0px; appearance: none; opacity: 0; transition: opacity 0.1s ease-in-out 0s; float: left; line-height: 18px; list-style: none;"><svg class="octicon octicon-smiley" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M1.5 8a6.5 6.5 0 1113 0 6.5 6.5 0 01-13 0zM8 0a8 8 0 100 16A8 8 0 008 0zM5 8a1 1 0 100-2 1 1 0 000 2zm7-1a1 1 0 11-2 0 1 1 0 012 0zM5.32 9.636a.75.75 0 011.038.175l.007.009c.103.118.22.222.35.31.264.178.683.37 1.285.37.602 0 1.02-.192 1.285-.371.13-.088.247-.192.35-.31l.007-.008a.75.75 0 111.222.87l-.614-.431c.614.43.614.431.613.431v.001l-.001.002-.002.003-.005.007-.014.019a1.984 1.984 0 01-.184.213c-.16.166-.338.316-.53.445-.63.418-1.37.638-2.127.629-.946 0-1.652-.308-2.126-.63a3.32 3.32 0 01-.715-.657l-.014-.02-.005-.006-.002-.003v-.002h-.001l.613-.432-.614.43a.75.75 0 01.183-1.044h.001z"></path></svg></summary></details>



[![@msftbot](https://avatars.githubusercontent.com/in/26612?s=60&v=4)](https://github.com/apps/msftbot) [msftbot](https://github.com/apps/msftbot) bot added [Needs-Triage](https://github.com/microsoft/terminal/labels/Needs-Triage) [Needs-Tag-Fix](https://github.com/microsoft/terminal/labels/Needs-Tag-Fix) labels [on 21 Feb](https://github.com/microsoft/terminal/issues/9237#event-4356409060)

[![@DHowett](https://avatars.githubusercontent.com/u/189190?s=88&v=4)](https://github.com/DHowett)

 

Member

### **[DHowett](https://github.com/DHowett)** commented [on 22 Feb](https://github.com/microsoft/terminal/issues/9237#issuecomment-782980992)

Thanks for letting us know. There's a bunch of discussion over in our [documentation repository](https://github.com/microsoftdocs/terminal) about this, so I'll have to redirect you there. Cheers!



[![@DHowett](https://avatars.githubusercontent.com/u/189190?s=60&v=4)](https://github.com/DHowett) [DHowett](https://github.com/DHowett) closed this [on 22 Feb](https://github.com/microsoft/terminal/issues/9237#event-4357109664)



[![@DHowett](https://avatars.githubusercontent.com/u/189190?s=60&v=4)](https://github.com/DHowett) [DHowett](https://github.com/DHowett) added [Issue-Docs](https://github.com/microsoft/terminal/labels/Issue-Docs) [Resolution-External](https://github.com/microsoft/terminal/labels/Resolution-External) labels [on 22 Feb](https://github.com/microsoft/terminal/issues/9237#event-4357109825)

[![@JustDre](https://avatars.githubusercontent.com/u/1915390?s=88&v=4)](https://github.com/JustDre)

 

### **[JustDre](https://github.com/JustDre)** commented [18 days ago](https://github.com/microsoft/terminal/issues/9237#issuecomment-798913706)

It seems the "Set-Theme" cmdlet was renamed to "Set-PoshPrompt".

👍 12❤️ 5🚀 2

<details class="details-overlay details-reset dropdown hx_dropdown-fullscreen position-relative float-left d-inline-block reaction-popover-container reactions-menu js-reaction-popover-container" style="box-sizing: border-box; display: inline-block !important; position: relative; float: left !important;"><summary class="btn-link reaction-summary-item add-reaction-btn" aria-label="Add your reaction" aria-haspopup="menu" role="button" style="box-sizing: border-box; display: inline-block; cursor: pointer; padding: 9px 15px 7px; font-size: inherit; color: var(--color-text-link); text-decoration: none; white-space: nowrap; user-select: none; background-color: initial; border: 0px; appearance: none; opacity: 0; transition: opacity 0.1s ease-in-out 0s; float: left; line-height: 18px; list-style: none;"><svg class="octicon octicon-smiley" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M1.5 8a6.5 6.5 0 1113 0 6.5 6.5 0 01-13 0zM8 0a8 8 0 100 16A8 8 0 008 0zM5 8a1 1 0 100-2 1 1 0 000 2zm7-1a1 1 0 11-2 0 1 1 0 012 0zM5.32 9.636a.75.75 0 011.038.175l.007.009c.103.118.22.222.35.31.264.178.683.37 1.285.37.602 0 1.02-.192 1.285-.371.13-.088.247-.192.35-.31l.007-.008a.75.75 0 111.222.87l-.614-.431c.614.43.614.431.613.431v.001l-.001.002-.002.003-.005.007-.014.019a1.984 1.984 0 01-.184.213c-.16.166-.338.316-.53.445-.63.418-1.37.638-2.127.629-.946 0-1.652-.308-2.126-.63a3.32 3.32 0 01-.715-.657l-.014-.02-.005-.006-.002-.003v-.002h-.001l.613-.432-.614.43a.75.75 0 01.183-1.044h.001z"></path></svg></summary></details>

[![@wys-wys](https://avatars.githubusercontent.com/u/63457826?s=88&u=a7ccd3874186cbdd9c4bc538a312e5aa238a355a&v=4)](https://github.com/wys-wys)

 

### **[wys-wys](https://github.com/wys-wys)** commented [6 minutes ago](https://github.com/microsoft/terminal/issues/9237#issuecomment-811691722)

It seems the "Set-Theme" cmdlet was renamed to "Set-PoshPrompt". thank you,i have solved it





[![@wys-wys](https://avatars.githubusercontent.com/u/63457826?s=80&v=4)](https://github.com/wys-wys)

Write Preview







 

Attach files by dragging & dropping, selecting or pasting them.

Comment