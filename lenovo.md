# Lenovo

## Lenovo Service Bridge
LSB.exe allows device detection from browser on Lenovo.com; it is installed in
`%APPDATA%\Local\Programs\Lenovo\Lenovo Service Bridge`.

If `LSB.exe` does not run it is because its HTTP ports 50128-50130 are occupied
by Hyper-V; to resolve:

* Disable Hyper-V: `dism.exe /Online /Disable-Feature:Microsoft-Hyper-V`
* Reserve LSB ports: `netsh int ipv4 add excludedportrange protocol=tcp startport=50128 numberofports=3`
* Re-enable Hyper-V: `dism.exe /Online /Enable-Feature:Microsoft-Hyper-V /All`
* Make Windows listen on all IPs: `netsh http add iplisten 0.0.0.0`
