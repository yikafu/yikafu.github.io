---
title: Powershell美化
author: yikafu
date: 2022-08-24 11:28:00
updated: 2022-08-24 11:28:00
tags: others
categories: 美化
cover:
---

# on my posh 的安装

1. 在微软商店搜索 `on my posh` 进行安装

2. 打开 PowerShell 提示符并运行以下命令：

   ```powershell
   winget install JanDeDobbeleer.OhMyPosh -s winget
   ```

3. 通过github下载安装包，安装最新版本的 `installxxx.exe`

   [Releases](https://github.com/JanDeDobbeleer/oh-my-posh/releases)



# 配置 PowerShell

Powershell版本需要6以上

推荐同时使用[Windows Terminal](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=zh-cn&gl=CN)

在 Powershell 中输入`notepad $PROFILE`，用记事本打开 Powershell 的配置文件脚本

当上述命令给出错误时，输入以下代码创建配置文件

```powershell
New-Item -Path $PROFILE -Type File -Force
```

输入`oh-my-posh init pwsh | Invoke-Expression` ，保存并关闭记事本

重新打开`Powershell`美化成功



# 更改主题

如果是默认安装在 `C:\Users\用户名\AppData\Local\Programs` ，使用`Get-PoshThemes`可以列出本地所有主题，否则需使用 `Get-PoshThemes -Path"安装目录路径"` ~~如C:\Program Files (x86)\oh-my-posh\themes~~



更改主题要打开 此电脑--文档--PowerShell 里面后缀名为 .ps1 的文件，将`oh-my-posh init pwsh | Invoke-Expression` , 改为` oh-my-posh init pwsh --config '安装目录+主题名.omp.json' | Invoke-Expression`



# 字体乱码

以管理员身份执行以下代码安装字体，或者通过其他方式安装 

```bash
oh-my-posh font install
```

然后在Powershell 或 Windows Terminal 中更改字体样式为 `MesloLGM NF`或其他Meslo字体

