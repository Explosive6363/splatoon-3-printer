# splatoon-3-printer
フォーク元のリポジトリをスプラトゥーン3でも動くようにしました。  
使用は自己責任でお願いします。

## 動作検証
### 必要なもの
- Aruduino UNO R3
- ジャンパーピン
- PC(確認時はArch Linux)

### 手順
#### 準備
##### Linux
- avr-libc
- avr-gcc  
をインストールしておく
ArchLinuxなら
```angular2html
yay -S avr-libc avr-gcc
```

##### Python
- pilow  
をインストール
```angular2html
pip3 install pillow
```
#### ビルド
1. ローカルのPCにこのリポジトリをcloneする。
   1. `git@github.com:Explosive6363/splatoon-3-printer.git`
2. 内包されているsubmoduleを最新化する
   1. `cd splatoon-3-printer`
   2. `git submodule update --init --recursive`
3. 320x120サイズのpng形式の画像を用意する。
4. 用意した画像をコンバートする
   1. `python3 png2c.py -p {用意した画像のpath}`
5. コンパイル
   1. `make`

#### Arduinoにバイナリを焼く
1. 画像の赤枠部分のピンをジャンプさせる
   1. ![PXL_20220914_060833015](https://user-images.githubusercontent.com/49982049/190075709-5ea909af-ed3d-4481-ba22-b3b421440ecd.jpg)
2. PCに接続する。
3. 1でジャンプさせたものを取り外す。
4. コマンド実行
   1. `sudo dfu-programmer atmega16u2 erase`
   2. `sudo dfu-programmer atmega16u2 flash Joystick.hex `
   3. `sudo dfu-programmer atmega16u2 reset`

### 使用
1. ゲーム内でポストに話しかける
2. 「投稿する」を押す
3. Lボタンを一回押す
4. switchのドックにArduinoを接続する
5. 完成を待つ
うまく行かない場合は「仕様」の手順を何回かやり直してみてください。
