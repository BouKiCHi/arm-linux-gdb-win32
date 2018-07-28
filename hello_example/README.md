# Raspberry Pi クロスデバッグ(vscode)

## 手順

* Raspberry Pi3にgdbserverをインストール
```
sudo apt-get install gdbserver
```

* .vscode/launch.jsonを次のように記述
```json:launch.json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/hello",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": true,
            "MIMode": "gdb",
            "miDebuggerPath": "${workspaceFolder}/bin/arm-linux-gnueabihf-gdb.exe",
            "setupCommands": [
                { "text": "target extended-remote raspi.local:9000" },
                { "text": "file ./hello" },
                { "text": "set remote exec-file ./hello" },
                { "text": "-enable-pretty-printing", "ignoreFailures": true }
            ]
        }
    ]
}
```
## ノート
* miDebuggerPathは適切なパスへ変更します
* setupCommandsのraspi.localはサーバ名なのでIPや適切な名前へ
* ポート番号(9000)はお好きな番号で

## その他
WinSCPなどで同期できるようにしておくと良いと思います。

## 実行
Raspberry Piのシェルで以下を実行します。
```
cd hello_example
gdbserver --multi :9000
```

vscodeでブレークポイントを設定し、デバッガの構成を選び実行します。


