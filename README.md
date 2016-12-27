# REVIVE USB チャタリング対策版（PID004A）
「REVIVE USB ver 007」と「REVIVE USB, Configuration Tool ver 1.30」をベースに作成したものです。  
一度だけボタンを押したつもりがダブルクリックになったりキーが複数回入力されるケース（チャタリング）を防ぐことが目的です。  
サンプリング方式とN回一致検出によるチャタリング防止を実現していて、ユーザがこれらのしきい値を変更することができます。  
## 使い方
基盤の組み立て方や配線などは下記を参考にしてください。  
URL: <http://a-desk.jp/modules/forum_module/index.php?cat_id=3> 

1. 上記URLからファームウェア書き込みソフト「HIDBootLoader.exe」をダウンロードして起動する。  

2. このリポジトリから「[REVIVE_USB_Debounce.hex](https://raw.githubusercontent.com/ushui/REVIVE_USB_Debounce/master/REVIVE_USB_Debounce.hex)」と「[REVIVE_USB_CT_for_Debounce.exe](https://github.com/ushui/REVIVE_USB_Debounce/raw/master/REVIVE_USB_CT_for_Debounce.exe)」をダウンロードする。  

3. 手持ちのREVIVE USBのショートピンをBOOTにしてPCへ接続する。  

4. 「Open Hex File」ボタンから「REVIVE_USB_Debounce.hex」を選択し、  
「Program/Velify」ボタンを押してREVIVE USBのファームウェアを書き換える。  
6. 手持ちのREVIVE USBのショートピンをBOOTから戻して再度PCへ接続する。  

7. 「REVIVE_USB_CT_for_Debounce.exe」を起動して好みの設定に変更する。  

## 設定ツールについて
「REVIVE USB, Configuration Tool ver 1.30」に手を加え、サンプリング周期と一致検出回数の設定項目を増やしたものです。  
チャタリング対策版ファームウェア以外では動作しません。  
デフォルトでは「サンプリング周期＝10ms／一致検出回数＝3回」に設定していますが、これらを変更することができます。  
### サンプリング周期
チャタリングノイズ除去の効果があります。  
1～174msまで設定可能で、その設定値ごとにスイッチのON/OFF読み出しを行います。  
長く設定すると長い間隔で読み出されるので、チャタリングが起こりにくくなる代わりに遅延が増加します。  
### 一致検出回数
ノイズ除去の効果があります。  
1～255回まで設定可能で、この設定値の回数分スイッチがONであれば正しい入力とみなします。  
大きく設定するとチャタリングノイズ除去の精度向上や外来ノイズの除去が期待できますが、サンプリング周期に比例して遅延が増加します。  

どの程度の設定値にすればよいかは使用するスイッチ・設置環境・用途によるので何とも言えません。  
一般的なマイクロスイッチであればデフォルト値から変更の必要はないと思われます。  
設定値の決め方は、設定ツールからキーボードと適当なキーに設定し、メモ帳を開いてボタンを押してチャタリングが確認できれば数値を上げてみる程度でいいと思います。  
もちろん遅延を抑えたい場合は逆のことを行えばいいでしょう。遅延秒数はおおよそサンプリング周期×一致検出回数で求められます（実際は少しブレます）。  
## 動作環境について
設定ツールはWindows XP以降のOSで動作します（Windows Vistaで動作を確認しています）。  
書き込み・設定をWindows上で行ってしまえば、ファームウェア（REVIVE USB）はMacやLinux/UNIX系のOSでも動作するはずです。
## 開発環境について
### ファームウェア
MPLAB IDE 8
### 設定ツール
Visual C# 2010 Express
## ソースコードについて
ライセンスは「Assembly Desk License」に準拠します。  
「REVIVE USB チャタリング対策版」は「REVIVE USB ver 007」と「REVIVE USB, Configuration Tool ver 1.30」をベースに、「REVIVE USB (Keyboard Only版) Ver 2.0.0」とその設定ツールを参考にして作成しました。  
作成者である「Bit Trade One, LTD」に感謝いたします。

***
2016/12/27 readme作成。
***
作成者： ushui（ゆーしゅい）  
Twitter: @kaede_hrc  
