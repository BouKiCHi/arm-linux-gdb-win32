# arm-linux-gnueabihf-gdb for win32

## 概要
Raspberry PiなどのコードをWindowsで動作するvscodeから、
gdbserver経由でクロスデバッグするためのバイナリです。
ソースコードには変更はありません。

## 使用方法

[Windows -> Raspberry Pi クロスデバッグ テンプレート](hello_example/README.md)

## ライセンス
ソースコード側に記載(GPL2)

## ソースコードの場所
ビルド手順に記載

## ビルド手順

msys2/mingw32でのビルド

参考 : https://qiita.com/take-iwiw/items/5b20558f8ab3f27ca4a4


### 追加インストールが必要(他にもあるかもしれません)
```
pacman -S texinfo
pacman -S expat
```

シェルで以下を実行
```
wget http://ftp.jaist.ac.jp/pub/GNU/gdb/gdb-8.0.1.tar.gz
tar xf gdb-8.0.1.tar.gz
cd gdb-8.0.1
mkdir build && cd build

 ../configure --target=arm-linux-gnueabihf --with-expat --without-python --enable-static --disable-interprocess-agent

make -j4
make LDFLAGS=-static -j4
# (インストール用は何かが違うみたいで、完了していてもコンパイルが始まる)

```

## 既知の不具合(known problems)
* コマンドプロンプトだとbackspaceなどが正しく表示されない
  
  →readline起因？


