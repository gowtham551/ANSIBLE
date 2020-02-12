# install & config of windows host

# Lunch windows server
 * Microsoft Windows Server 2012 Base

 **PowerShell Upgrade into 5.1**

 ```
 ON WIN HOST: 

 $url = "https://raw.githubusercontent.com/jborean93/ansible-windows/master/scripts/Upgrade-PowerShell.ps1"
$file = "$env:temp\Upgrade-PowerShell.ps1"
$username = "Administrator"
$password = "Password"

(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force

# Version can be 3.0, 4.0 or 5.1
&$file -Version 5.1 -Username $username -Password $password -Verbose

 ```

 **ConfigureRemotingForAnsible**

 ```
ON WIN HOST:

$url = "https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1"
$file = "$env:temp\ConfigureRemotingForAnsible.ps1"

(New-Object -TypeName System.Net.WebClient).DownloadFile($url, $file)

powershell.exe -ExecutionPolicy ByPass -File $file

 ```
**WinRM Listener**

 ```
winrm enumerate winrm/config/Listener
 ```

 **ON Ansible Server side**

```
# apt-get update
# apt-get install python-pip
# pip install "pywinrm>=0.3.0"
```

**winHosts**
```
[win]
172.31.25.64

[win:vars]
ansible_user=Administrator
ansible_password=bf36foAA8mf
ansible_connection=winrm
ansible_winrm_server_cert_validation=ignore

```

> ansible all -i winhosts -m win_ping

> ansible-playbook -i winhosts winplaybook.yml