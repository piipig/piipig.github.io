---
layout: post
title:  "rm後還是有機會的"
date:   2018-04-02 18:16:31 +0800
categories: linux update
---

* content
{:toc}

## <font color="SaddleBrown">前言</font>
因為不小心從遠端下了rm把本地端的資料，尤其是程式檔給清個屍骨無存QQ，花了快一個禮拜的時間，實在很不想再重打，所以只好上網找解藥，沒想到還真的有！！雖然沒有全數救回，但沒有完全空手，我已經感動涕零，立馬打了這篇

### <font color="SaddleBrown"> 使用軟體 -- extundelete </font>
> extundelet是免費開源的工具，我自己本身是在ext4檔案系統救援成功，爬文的網址也有提及ext3

<br>

#####下載＆安裝
```
sudo apt install extundelete
```
##### 救援檔案
先找到檔案所在目錄的inode
```
ls -id filepath
```
接著找出這個檔案位在哪個dev裝置路徑下，假設是在/dev/sda1下

```
df filepath
```

```
lsblk
```

找到以後就可以透過extundelete先檢查檔案狀態
```
sudo extundelete /dev/sda1 --inode indoenumber
```
此時會跳出一些警告訊息，按y繼續將會看到一長串的清單，刪除後的檔案，會看到其Deleted Status為Deleted
接下來就可以開始救援的工作了
```
sudo extundelete /dev/sda1 --restore-file filepath
```
<font color="Crimson">Notice: </font> --restore-file 之後接的檔案路徑是從裝置掛載點算起，而不是檔案的絕對路徑 

如果是要救援整個資料夾的話只要把最後救援的指令的--restore-file改成 --restore-director
```
sudo extundelete /dev/sda1 --restore-director dirPath
```
