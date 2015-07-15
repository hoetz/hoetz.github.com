---
layout: post
category : exchange
tagline:
date: 2015-07-15 08:00:00 UTC 
tags : [exchange,powershell]
title: Remove and block a mobile device with Exchange Powershell
---
{% include JB/setup %}

Occasionally you want to remove an employee's active sync device and block it for good. Calling "Remove-MobileDevice" will remove the device partnership
but it will come back if it's already been added to the allowed devices of the mailbox. In the example below, I want to get rid of a user's Android devices,
so I'm adding those DeviceIDs to the list of blocked IDs on the Mailbox before I remove the device from the system.

	$EXCHANGE_SESSION_NAME = "ExchangeSession"
	
	function Create-ExchangePowershellSession()
	{
	    $PsSession = New-PSSession -ConfigurationName Microsoft.Exchange -Name $EXCHANGE_SESSION_NAME -ConnectionUri http://ExchangePS.yourdomain.com/PowerShell -Authentication Kerberos
	    Import-PSSession $PsSession
	}
	
	function Remove-ExchangePowershellSession()
	{
	    Remove-PSSession -Name $EXCHANGE_SESSION_NAME
	}
	
	Create-ExchangePowershellSession
	
	$casIdentity="joe.toblock@yourdomain.com"
	
	$EASDeviceStats = @(Get-MobileDeviceStatistics -Mailbox $casIdentity)
	
	  Foreach ($EASDevice in $EASDeviceStats)
	  {
		 if ($EASDevice.DeviceOS -eq "Android")
		 {
		     $deviceGuid=[string]$EASDevice.Guid
			 
		     $deviceID=$EASDevice.DeviceID
		
		     Set-CASMailbox -Identity $casIdentity -ActiveSyncAllowedDeviceIDs @{REMOVE=$deviceID} -ActiveSyncBlockedDeviceIDs @{ADD=$deviceID}
		
		     Remove-MobileDevice -Identity $deviceGuid -Confirm:$False
	     }
	  }
	
	Remove-ExchangePowershellSession









