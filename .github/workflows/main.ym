
name: SAKUTOPUP-FREE-3H
on:
workflow_dispatch:
jobs:
deployment:
runs-on: windows-latest
timeout-minutes: 180 # Dikunci ke 3 Jam agar akun lebih awet
steps:
- name: 1. System Preparation
run: |
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -Name "fDenyTSConnections" -Value 0 -Force
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -Name "UserAuthentication" -Value 0 -Force
netsh advfirewall firewall set rule group="remote desktop" new enable=Yes
Restart-Service -Name TermService -Force
- name: 2. Identity Generation (Random)
run: |
$id = Get-Random -Minimum 1000 -Maximum 9999
$u = "UserSAKU$id"
# Password Aman & Stabil (Besar, Kecil, Angka)
$sets = @("ABCDEFGHJKLMNPQRSTUVWXYZ", "abcdefghijkmnpqrstuvwxyz", "23456789")
$p = ""
foreach ($s in $sets) { $p += $s[(Get-Random -Maximum $s.Length)] }
$all = -join $sets
for ($i=1; $i -le 11; $i++) { $p += $all[(Get-Random -Maximum $all.Length)] }
echo "SAKU_USER=$u" >> $env:GITHUB_ENV
echo "SAKU_PASS=$p" >> $env:GITHUB_ENV
net user $u $p /add /y
net localgroup Administrators $u /add
- name: 3. Deploy Branding
run: |
$Desktop = "C:\Users\Public\Desktop"
$Shell = New-Object -ComObject WScript.Shell
$Shortcut = $Shell.CreateShortcut("$Desktop\SAKUTOPUP-WEB.url")
$Shortcut.TargetPath = "https://sakutopup.gamesquad.id/"
$Shortcut.Save()
- name: 4. Secure Tunneling
run:
