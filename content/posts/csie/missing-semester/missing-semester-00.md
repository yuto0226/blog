---
title: Before the Course
date: 2022-09-26 17:29:58
cover:
top_img:
categories: 
    - [計算機科學, ./missing-semester]
tags:
    - 'Shell'
    - 'Linux'
---
課程裡面所使用的環境都是類UNIX系統。如果你是Windows系統的話就要用WSL來模擬LINUX的環境，而且可能會有很多東西跟教授所講的不太一樣。接下來會用Windows 11操作。

:::warning
Windows 10 版本必須是 2004 (19041.450) 以上
:::
# Windows Terminal
一個可以讓你Terminal漂漂亮亮的東西
[Microsoft Store的連結](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=zh-tw&gl=tw)

# Windows 功能
直接去搜尋打上`Windows 功能`並點開
![](https://i.imgur.com/06yRB0p.png)

把裡面的`Windows 子系統 Linux 版`跟`虛擬機平台`勾起來
![](https://i.imgur.com/wvDuRaG.png)

開啟WindowsTerminal(Power Shell或命令提示字元都可以)
```bash Windows Terminal command:("[root@localhost] $":1)
wsl --install
著作權 (c) Microsoft Corporation。保留擁有權利。

使用方式: wsl.exe [Argument] [Options...] [CommandLine]

用於執行 Linux 二進位檔的引數:

    如果未提供任何命令列，wsl.exe 會啟動預設的殼層。

    --exec, -e <CommandLine>
        執行指定的命令，但不使用預設的 Linux 殼層。

    --
        依原樣傳遞剩餘的命令列。

選項:
    --cd <Directory>
        將指定的目錄設定為目前的工作目錄。
        如果使用 ~，將會使用 Linux 使用者的主目錄路徑。如果該路徑的開頭
        為 / 字元，將會解譯為絕對 Linux 路徑。
        否則，該值必須是絕對 Windows 路徑。

    --distribution, -d <Distro>
        執行指定的發佈。

    --user, -u <UserName>
        以指定使用者的身分執行。

    --system
        啟動系統發佈的殼層。

用於管理 Windows 子系統 Linux 版的引數:

    --help
        顯示使用資訊。

    --install [Options]
        安裝其他 Windows 子系統 Linux 版發佈。
        如需有效發佈的清單，請使用 'wsl --list --online'。

        選項:
            --distribution, -d [Argument]
                依名稱下載並安裝發佈。

                引數:
                    有效發佈名稱 (不區分大小寫)。

                範例:
                    wsl --install -d Ubuntu
                    wsl --install --distribution Debian

    --set-default-version <Version>
        針對新發佈變更預設安裝版本。

    --shutdown
        立即終止所有執行中的發佈和 WSL 2
        輕量公用程式虛擬機器。

    --status
        顯示 Windows 子系統 Linux 版狀態。

    --update [Options]
        如果未指定選項，則會更新 WSL 2 核心
        至最新版本。

        選項:
            --rollback
                還原至舊版 WSL 2 核心。

在 Windows 子系統 Linux 版中用於管理發佈的引數:

    --export <Distro> <FileName>
        將發佈匯出為 tar 檔案。
        檔案名稱可以是 - 以用於標準輸出。

    --import <Distro> <InstallLocation> <FileName> [Options]
        匯入指定的 tar 檔案作為新發佈。
        檔案名稱可以是 - 以用於標準輸入。

        選項:
            --version <Version>
                指定要用於新發佈的版本。

    --list, -l [Options]
        列出發佈。

        選項:
            --all
                列出全部發佈，包含
                正在安裝或解除安裝的發佈。

            --running
                只列出目前正在執行的發佈。

            --quiet, -q
                只顯示發佈名稱。

            --verbose, -v
                顯示所有發佈的詳細資訊。

            --online, -o
                顯示可用發佈的清單，以使用 'wsl --install' 安裝。

    --set-default, -s <Distro>
        將發佈設定為預設值。

    --set-version <Distro> <Version>
        變更所指定發佈的版本。

    --terminate, -t <Distro>
        終止指定的發佈。

    --unregister <Distro>
        取消登錄發佈並刪除根檔案系統。

    --mount <Disk>
        在所有 WSL2 發佈中連結並裝載實體磁碟。

        選項:
            --bare
                將磁碟連結到 WSL2，但不要裝載磁碟。

            --type <Type>
                裝載磁碟時要使用的檔案系統，若未指定，預設為 ext4。

            --options <Options>
                其他裝載選項。

            --partition <Index>
                要裝載之磁碟分割的索引，若未指定，預設為整個磁碟。

    --unmount [Disk]
        從所有 WSL2 發佈卸載並中斷連結磁碟。
        若在沒有引數的情況下呼叫，即卸載並中斷連結所有磁碟。
```
可以用參數`-l -o`把所有發行版都印出來
```bash Windows Terminal command:("[root@localhost] $":1)
wsl -l -o
以下是可安裝之有效發佈的清單。
使用 'wsl --install -d <Distro>' 安裝。

NAME            FRIENDLY NAME
Ubuntu          Ubuntu
Debian          Debian GNU/Linux
kali-linux      Kali Linux Rolling
openSUSE-42     openSUSE Leap 42
SLES-12         SUSE Linux Enterprise Server v12
Ubuntu-16.04    Ubuntu 16.04 LTS
Ubuntu-18.04    Ubuntu 18.04 LTS
Ubuntu-20.04    Ubuntu 20.04 LTS
```
挑自己喜歡的版本按照上面給的提示安裝，以Ubuntu為例:
```bash Windows Terminal command:("[root@localhost] $":1)
wsl --install -d Ubuntu
```
