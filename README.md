# Get-AzVMContainerID
Some PowerShell examples on how to reach out to Azure WireServer from a VM or VMSS instance to get the ContainerID from Azure platform.


### Using Invoke-RestMethod
```PowerShell
$uri = 'http://168.63.129.16/machine?comp=goalstate'
$headers = @{
    "x-ms-guest-agent-name" = "WaAgent-2.5.0.0 (2.7.0.0)"
    "x-ms-version" = "2015-04-05"
}
$xml = $null
$xml = Invoke-RestMethod -Uri $uri -Headers $headers
$xml.GoalState.Container.ContainerId
```


### Using System.Net.WebClient class
```PowerShell
$uri = 'http://168.63.129.16/machine?comp=goalstate'
$wc = New-Object System.Net.WebClient 
$wc.Headers.Add("x-ms-guest-agent-name", "WaAgent-2.5.0.0 (2.7.0.0)")
$wc.Headers.Add("x-ms-version", "2015-04-05")
$xml = $null
$xml = [xml]$wc.DownloadString($uri)
$xml.GoalState.Container.ContainerId
```
