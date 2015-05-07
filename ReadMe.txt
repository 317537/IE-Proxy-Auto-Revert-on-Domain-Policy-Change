# Date:     23rd January 2012
# Author:   Leslie Fleming
# Summary:  Text Document describing each file in summary.
# Note:     Running 'PsUpdateIEProxySettings.ps1' will create a task in TaskScheduler (taskschd.msc) which runs
#           every five minutes to undo domain proxy ip changes. This is intended for situations where the default proxy
#           IP needs to be replaced for a less restrictive proxy IP.
#           The default folder for testing is C:\Temp\IEProxySettings and can be changed to a more desired location.


To initiate the task (clean setup) execute PsUpdateIEProxySettings.ps1. This will setup the task to run the vbscript file.

1. ReadProxySettings.cs
   The un-compiled C# code, for the notification to IE of proxy changes.
  
2. IEProxyRefresh.dll
   The compiled C# code of the ReadProxySettins.cs file.
  
3. PsUpdateIEProxySettins.ps1
   A power-shell script which is the main entry point for the automated update of Internet Explorer
   proxy settings. Add the preferred proxy IP and ignore proxy details for local subnets here.
  
4. ModCreateProxySettings.psm1
   The module responsible for the registry updates relating to IE proxy details.
   
5. ModReadProxySettings.psm1
   The module responsible for notifying IE of a change to the proxy settings. It essentially saves me having to close
   down IE in order for it to refresh (read registry) for proxy details.
   
6. Proxy.vbs
   A vbScript file which is run by a newly created scheduled task, which in turn 
   invokes the power-shell cmdlet 'PsUpdateIEProxySettins.ps1'. The vbScript ensures that the 
   taskeng.cmd window is run in 'hidden' mode when the task executes under the current logged in user
   context. This is not necessary if the scheduled task runs under a service account or another user context.