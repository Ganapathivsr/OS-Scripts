# To setup Auditing -------
write-host Setting up Auditing

$folders = Get-Content ".\Powershell\Folders.txt"
$User = "Everyone"
$Rules = "FullControl"
$InheritType = "None"
$AuditType = "Failure"
$hostn = hostname

write-host "$hostn"
foreach($folder in $folders)
{
$ACL = new-object System.Security.AccessControl.DirectorySecurity
$AccessRule = New-Object System.Security.AccessControl.FileSystemAuditRule($user,$Rules,$InheritType,"None",$AuditType)
$ACL.SetAuditRule($AccessRule)
$ACL | Set-Acl $Folder
write-host "Setting Audit Rules on $folder"
}

