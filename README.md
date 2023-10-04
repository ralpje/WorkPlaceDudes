# WorkPlaceDudes Meetup October 4th, 2023

Thanks for visiting the (https:/www.workplacedudes.nl)[Workplacedudes] meetup!
The (m365dsc.pptx)[slides] can be found on my Github repository.

If you want help with your journey on using (https://microsoft365dsc.com/)[Microsoft365DSC], visit the product website. There, you can also find the h(ttps://office365dsc.azurewebsites.net/Pages/Resources/Whitepapers/Managing%20Microsoft%20365%20with%20Microsoft365Dsc%20and%20Azure%20DevOps.pdf)[whitepaper] on integrating M365DSC with Azure DevOps.

Finaly, below are the code snippets used during my presentation
```powershell

# Auth Settings
$CertificateThumbprint = "CertThumbprint goes here"
$ApplicationID = "App ID goes here"
$Tenantid = "<tenantname>.onmicrosoft.com" 

# Exporting AADApplications using certificate
Export-M365DSCConfiguration -Components @("AADApplication") -ApplicationId $ApplicationId -CertificateThumbprint $CertificateThumbprint -TenantId $TenantId

# Combining options for export
Export-M365DSCConfiguration -Workloads "AAD" -ApplicationID $ApplicationID -CertificateThumbprint $CertificateThumbprint -TenantId $Tenantid -filename AAD.ps1 -configurationname AAD -Path c:\Demo\WorkplaceDudes

# Export configs of specific settings
Export-M365DSCConfiguration -Components 'AADConditionalAccessPolicy' -ApplicationId $ApplicationId -CertificateThumbprint $CertificateThumbprint -TenantId $TenantId -FileName ConditionalAccess.ps1 -Path c:\demo\workplacedudes

# Generate Delta
New-M365DSCDeltaReport -Source C:\demo\aad_baseline.ps1 -Destination C:\demo\workplacedudes\aad.ps1 -OutputPath c:\demo\workplacedudes\delta.html

# Generate a Configuration Report
New-M365DSCReportFromConfiguration -Type excel -ConfigurationPath C:\demo\workplacedudes\ConditionalAccess.ps1 -OutputPath c:\demo\workplacedudes\Report.xlsx

# Compiling the MOF file from Configuration export
set-location C:\demo\WorkplaceDudes
.\ConditionalAccess.ps1

# Applying the DSC Config
Start-DSCConfiguration -Path C:\demo\workplacedudes\conditionalaccess -Wait -Verbose -Force

# Stop Config

Stop-DSCConfiguration -Force
Remove-DSCConfigurationDocument -Stage Current

```



If you have any furhter questions, reach out to me on (https://twitter.com/ralpje)[Twitter / X], (https://linkedin.com/in/ralpheckhard)[LinkedIn], or by contacting me through my (https://ralpheckhard.com)[website].

Have fun managing your M365 setup as code!
