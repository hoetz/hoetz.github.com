---
layout: post
category : android
tagline: 
tags : [android, tfs, eclipse, install]
---
{% include JB/setup %}

Since I inherited an Android project, I had to do a clean install of the development tools on my Windows 8 machine including the Team Foundation Server Plugin for Eclipse.

Here are my notes:

- The latest Development Tools for Android (including Eclipse) can be found [here](http://developer.android.com/sdk/index.html)
- To enable Android debugging on physical devices, download the USB driver for your cellphone, look [here](http://developer.android.com/tools/device.html)
- The driver for Samsung devices can be obtained via the samsung kies software
- Download and install the Team Foundation Server Plug In with [this guide](http://msdn.microsoft.com/en-us/library/hh301122.aspx)
- In Eclipse go to Window -> Preferences -> Team -> Team Foundation Server
- Check “accept untrusted SSL certificates” (couldn’t get it to work otherwise)
- In Eclipse go to Window -> Open Perspective -> Other -> Team Foundation Server
- Add your TFS address
- Get a project or add some sources to the TFS
- To get an integrated TFS experience with your project:
	- Right click on your project in the package explorer
	- Team -> Share Project -> Team Foundation Server
	- This enables TFS as the source control plug-in



