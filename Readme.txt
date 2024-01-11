Windows調整預設防毒CPU使用占比(Windows adjusts default antivirus CPU usage ratio)

調整預設防毒原來CPU使用率佔比(50%->5%)
https://www.kocpc.com.tw/archives/528487
https://www.majorgeeks.com/content/page/how_to_change_windows_defender_max_cpu_usage.html

方案01.[GUI操作]
01.使用「Win + R」快捷鍵打開搜尋功能，輸入「gpedit.msc」並按下確定，就能打開「本機群組原則編輯器」

02.打開電腦設定 -> 系統管理範本 -> Windows 元件 -> Microsoft Defender 防毒軟體 -> 掃描，接著右邊可以找到「指定掃描期間的 CPU 使用率百分比上限」，點兩下打開

03.將下方「指定掃描期間的 CPU 使用率百分比上限」數字改成你想要的，可以設定 5 到 100，預設為 50，如果你想要調低，就是變成 5~50 之間的數字，最低就 5。設定完成之後，每當 Microsoft Defender 啟用自動掃描時，就不會超過這個百分比。輸入完畢後，按套用、確定，這樣就完成了

04.重新開機

方案02.[指令操作]
01.使用管理者權限開啟PowerShell 再命令列 輸入 下列命令:『Get-MpPreference | select ScanAvgCPULoadFactor』查詢修改結果

02.使用管理者權限開啟PowerShell 再命令列 輸入 下列命令:『Set-MpPreference -ScanAvgCPULoadFactor 5』使用指令再修改一次

03.重新開機


===
Windows家用版找不到 *本機群組原則編輯器* 要用這一篇 先把該功能啟用
https://www.gdaily.org/13719/%E5%A6%82%E4%BD%95%E6%89%BE%E5%9B%9E-gpedit-msc-%E6%9C%AC%E6%A9%9F%E7%BE%A4%E7%B5%84%E5%8E%9F%E5%89%87%E7%B7%A8%E8%BC%AF%E5%99%A8-win7-win8-win10

@echo off
pushd "%~dp0"
dir /b %SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientExtensions-Package~3*.mum >List.txt
dir /b %SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientTools-Package~3*.mum >>List.txt
for /f %%i in ('findstr /i . List.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
pause