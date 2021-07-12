### Windows Power Shell常用命令

暂时可以先参考：[https://www.cnblogs.com/feng-zhizi/p/9935874.html](https://www.cnblogs.com/feng-zhizi/p/9935874.html)

在windows power shell中，文件/夹的移除，通过remore-item命令，我们可以先看下关于这个命令的简单介绍。

```bash
D:> get-help remove-item -full

名称
    Remove-Item

语法
    Remove-Item [-Path] <string[]>  [<CommonParameters>]

    Remove-Item  [<CommonParameters>]


参数
    -Confirm

        是否必需?                    False
        位置?                        已命名
        是否接受管道输入?            False
        参数集名称          (所有)
        别名                     cf
        动态?                    false

    -Credential <pscredential>

        是否必需?                    False
        位置?                        已命名
        是否接受管道输入?            True (ByPropertyName)
        参数集名称          (所有)
        别名                     无
        动态?                    false

    -Exclude <string[]>

        是否必需?                    False
        位置?                        已命名
        是否接受管道输入?            False
        参数集名称          (所有)
        别名                     无
        动态?                    false

    -Filter <string>

        是否必需?                    False
        位置?                        已命名
        是否接受管道输入?            False
        参数集名称          (所有)
        别名                     无
        动态?                    false

    -Force

        是否必需?                    False
        位置?                        已命名
        是否接受管道输入?            False
        参数集名称          (所有)
        别名                     无
        动态?                    false

    -Include <string[]>

        是否必需?                    False
        位置?                        已命名
        是否接受管道输入?            False
        参数集名称          (所有)
        别名                     无
        动态?                    false

    -LiteralPath <string[]>

        是否必需?                    True
        位置?                        已命名
        是否接受管道输入?            True (ByPropertyName)
        参数集名称          LiteralPath
        别名                     PSPath
        动态?                    false

    -Path <string[]>

        是否必需?                    True
        位置?                        0
        是否接受管道输入?            True (ByValue, ByPropertyName)
        参数集名称          Path
        别名                     无
        动态?                    false

    -Recurse

        是否必需?                    False
        位置?                        已命名
        是否接受管道输入?            False
        参数集名称          (所有)
        别名                     无
        动态?                    false

    -Stream <string[]>

        是否必需?                    False
        位置?                        已命名
        是否接受管道输入?            False
        参数集名称          (所有)
        别名                     无
        动态?                    true

    -UseTransaction

        是否必需?                    False
        位置?                        已命名
        是否接受管道输入?            False
        参数集名称          (所有)
        别名                     usetx
        动态?                    false

    -WhatIf

        是否必需?                    False
        位置?                        已命名
        是否接受管道输入?            False
        参数集名称          (所有)
        别名                     wi
        动态?                    false

    <CommonParameters>
        此 Cmdlet 支持常见参数: Verbose、Debug、
        ErrorAction、ErrorVariable、WarningAction、WarningVariable、
        about_CommonParameters (https:/go.microsoft.com/fwlink/?LinkID=113216)。


输入
    System.String[]
    System.Management.Automation.PSCredential


输出
    System.Object

别名
    ri
    rm
    rmdir
    del
    erase
    rd


备注
    Get-Help 在此计算机上找不到该 cmdlet 的帮助文件。它仅显示部分帮助。
        -- 若要下载并安装包含此 cmdlet 的模块的帮助文件，请使用 Update-Help。
        -- 若要联机查看此 cmdlet 的帮助主题，请键入: "Get-Help Remove-Item -Online" 或
           转到 https://go.microsoft.com/fwlink/?LinkID=113373。
```