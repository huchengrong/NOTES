# 防火墙

```clike
1. 关闭防火墙
Set-MpPreference -disablerealtimeMonitoring $true
2. 查看防火墙状态
powershell -c Get-NetFirewallRule -Direction Outbound -Enabled True -Action Block 
3. 查看详细防火墙策略
powershell -c "Get-NetFirewallRule -Direction Outbound -Enabled True -Action Block | Format-Table -Property DisplayName, @{Name='Protocol';Expression={($PSItem | Get-NetFirewallPortFilter).Protocol}},@{Name='LocalPort';Expression={($PSItem | Get-NetFirewallPortFilter).LocalPort}},@{Name='RemotePort';Expression={($PSItem | Get-NetFirewallPortFilter).RemotePort}},@{Name='RemoteAddress';Expression={($PSItem | Get-NetFirewallAddressFilter).RemoteAddress}},Enabled,Profile,Direction,Action"
4. 寻找例外的防火墙
powershell -c Get-NetFirewallRule -Direction Outbound -Enabled True -Action Allow
```
