# REVIVE USB チャタリング対策版（PID004A）
一度しかボタンを押していないのにダブルクリックになる、キーが複数回入力されるなどのケースを防ぐことができます。  
通常のファームウェアはリアルタイムでスイッチの状態を読み取っているのでわずかな信号の揺れも検知してしまいますが、これを一定時間ごとに読み取って解決しています。  
そのため遅延（デフォルトは最短30ms。1～44370msまで調整可）が生じることに注意が必要です。  
設定ツールによってしきい値を変更できるので、遅延を抑えたい場合やそれでもチャタリングが起きる場合にも対応できます。  
## 使い方
基盤の組み立て方や配線などは下記を参考にしてください。  
URL: <http://a-desk.jp/modules/forum_module/index.php?cat_id=3> 

1. 上記URLからファームウェア書き込みソフト「HIDBootLoader.exe」をダウンロードする。  

2. このリポジトリから「[REVIVE_USB_Debounce_latest.zip](https://github.com/ushui/REVIVE_USB_Debounce/raw/master/REVIVE_USB_Debounce_latest.zip)」をダウンロードし、解凍する。  
「readme.txt」「REVIVE_USB_Debounce_CT.exe」「REVIVE_USB_Debounce_FW.hex」の3つのファイルが解凍される。  

3. 手持ちのREVIVE USBのショートピンをBOOTにしてPCへ接続する。  

4. 「HIDBootLoader.exe」を起動して「Open Hex File」ボタンから「REVIVE_USB_Debounce_FW.hex」を選択し、  
「Program/Velify」ボタンを押してREVIVE USBのファームウェアを書き換える。  
6. REVIVE USBのショートピンをBOOTから戻して再度PCへ接続する。  

7. 「REVIVE_USB_Debounce_CT.exe」を起動して好みの設定に変更する。  

## 設定ツールについて
「REVIVE USB, Configuration Tool」にサンプリング周期と一致検出回数の設定項目を増やしたものです。  
当ファームウェア以外では動作しません。  
デフォルトでは「サンプリング周期＝10ms／一致検出回数＝3回」に設定していますが、必要であれば変更することができます（そのままでも使えます）。  

![REVIVE USB Debounce, Configuration Tool](https://raw.githubusercontent.com/ushui/REVIVE_USB_Debounce/master/revive_usb_debounce_ct.png)  
### サンプリング周期
チャタリングノイズ除去の効果があります。  
1～174msまで設定可能で、その設定値ごとにスイッチのON/OFF読み出しを行います。  
長く設定すると長い間隔で読み出されるので、チャタリングが起こりにくくなる代わりに遅延が増加します。  
### 一致検出回数
ノイズ除去の効果があります。  
1～255回まで設定可能で、その回数分スイッチがONであれば正しい入力とみなして入力を行います。  
ONからOFFになる時にも回数分OFFであることを確認します。  
大きく設定するとチャタリングノイズ除去の精度向上や外来ノイズの除去が期待できますが、サンプリング周期に比例して遅延が増加します。  
### 補足
どの程度の設定値にすればよいかは使用するスイッチ・設置環境・用途によるので何とも言えません。  
一般的なマイクロスイッチであればデフォルト値から変更の必要はないと思われます。  
設定値の決め方は、設定ツールからキーボードと適当なキーに設定し、メモ帳を開いてボタンを押してチャタリングが確認できれば数値を上げてみる程度でいいと思います。  
もちろん遅延を抑えたい場合は逆のことを行えばいいでしょう。遅延秒数は**サンプリング周期×一致検出回数**で求められます（最短の時間です。実際は後ろに少しブレます）。  
## 動作環境について
設定ツールはWindows XP以降のOSで動作します（Windows Vistaで動作を確認しています）。  
書き込み・設定をWindows上で行ってしまえば、ファームウェア（REVIVE USB）はMacやLinux/UNIX系のOSでも動作するはずです。
## 開発環境・開発言語について
### ハードウェア
REVIVE USB (PIC18F14K50)
### ファームウェア
開発環境：MPLAB IDE 8  
開発言語：C
### ソフトウェア（設定ツール）
開発環境：Visual C# 2010 Express  
開発言語：C#
## ソースコードについて
「Assembly Desk License」ライセンスに準拠します。  
「REVIVE USB チャタリング対策版」は「REVIVE USB」と「REVIVE USB, Configuration Tool」をベースに、「REVIVE USB (Keyboard Only版) 」とその設定ツールを参考にして作成しました。作成者である「Bit Trade One, LTD」に感謝いたします。
## 派生バージョン
* [REVIVE USB MATRIX チャタリング対策版（PID004B）](https://github.com/ushui/REVIVE_USB_MATRIX_Debounce)
* [REVIVE USB ロータリーエンコーダ対応 チャタリング対策版（PID004C）](https://github.com/ushui/REVIVE_USB_RENC_Debounce)

***
2017/01/04 ロータリーエンコーダ対応版に合わせて表記の追記と修正。  
2017/01/01 MATRIX版に合わせて表記の追記と修正。  
2016/12/29 FW Version 1.2に合わせて追記。  
2016/12/28 文書の追記と補足・修正。使い方の手順を書き換えた。  
2016/12/27 readme作成。
***
作成者： ushui（ゆーしゅい）  
Twitter: [@kaede_hrc](https://twitter.com/kaede_hrc)  
