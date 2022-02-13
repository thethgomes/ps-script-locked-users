# ps-script-locked-users
_Power Shell to identify users locked out in Active Directory and send an e-mail notification to sysadmin_

```
#Getting User locked event from Active Directory, ID: 4740
$A = Get-WinEvent -MaxEvents 1 -FilterHashTable @{LogName='Security';ID='4740'} | Select-Object -Property *
$EmailFrom = "dc-contoso@contoso.com"
$EmailTo = "tilockedout@contoso.com"
$Subject = "Usuario Bloqueado!!!"
$Body = $A 
# you may need to inform local mail server IP address from your exchange server
$SMTPServer = "192.168.0.1"
Send-MailMessage -From $EmailFrom -To $EmailTo -Subject $Subject -body ($Body | Out-String) -SmtpServer $SMTPServer
``` 
