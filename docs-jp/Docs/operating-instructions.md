<p align="right">
            別の言語で表示: <a href="../../Docs/operating-instructions.md">英語</a>    <table style="width:100%"><table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>reVISION 入門ガイド 2018.3 (UG1265)</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center"><a href="../README.md">1. はじめに</a></td>
    <td width="16%" align="center"><a href="overview.md">2. 概要</a></td>
    <td width="17%" align="center"><a href="software-tools-system-requirements.md">3. ソフトウェア ツールおよびシステム要件</a></td>
    <td width="17%" align="center"><a href="design-file-hierarchy.md">4. デザイン ファイルの階層</a></td>
</tr>
<tr>
    <td width="17%" align="center">5. インストールおよび操作手順</td>
    <td width="16%" align="center"><a href="tool-flow-tutorials.md">6. ツール フロー チュートリアル</a></td>
    <td width="17%" align="center"><a href="run-application.md">7. アプリケーションの実行</a></td>
    <td width="17%" align="center"><a href="platform-details.md">8. プラットフォームの詳細</a></td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="known-issues-limitations.md">9. 既知の問題および制限</a></td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. その他のリソース</a></td>
</tr>
</table>

# 5. インストールおよび操作手順

## 5.1. ボード設定
### 5.1.1. シングル センサーの設定

##### 5.1.1.1. 必要な操作
* 電源を 12V 電源コネクタに接続します。
* ディスプレイ オプション (次のいずれかを選択):
  * DisplayPort ケーブルの一端をボードの DisplayPort コネクタに、もう一端をモニターに接続します。
  * HDMI ケーブルの一端をボードの HDMI 出力に、もう一端をモニターに接続します。

**:warning: 警告:** ボードの DisplayPort または HDMI 出力のいずれかのみを接続してください。両方接続すると、デザインが誤動作する可能性があります。

**:pushpin: 注記:** モニターによっては、異なる HDMI 規格をサポートするため複数の HDMI ポートがあるものもあります。4k60 パフォーマンスには、HDMI 2.0 対応ポート (使用可能な場合) を選択してください。

* マイクロ USB ケーブルを USB-UART コネクタに接続します。ターミナル エミュレーターに次の設定を使用します。
  * ボー レート: 115200
  * データ: 8 ビット
  * パリティ: なし
  * ストップ: 1 ビット
  * フロー制御: なし

* 次のいずれかのディレクトリからコピーしたビルド済みイメージを含む SD カード (FAT フォーマット) を挿入します。
  * `sd_card/optical_flow`
  * `sd_card/stereo`
  * `sd_card/filter2d`
  * `sd_card/triple`

##### 5.1.1.2. オプションの操作
* HDMI ケーブルの一端をボードの HDMI 入力 (下の HDMI コネクタ) に、もう一端を HDMI ソースに接続します。
* See3CAM_CU30 または ZED USB カメラをザイリンクス USB3 マイクロ B アダプターを介して USB3 マイクロ AB コネクタに接続します。
* LI-IMX274MIPI-FMC モジュールをボードの FMC コネクタに接続します (ZCU102 の HPC0 コネクタを使用)。

  **:pushpin: 注記:** ドーター カードの接続には、VADJ を **1.2V** に設定する必要があります。FMC カードが機能しない場合は、rev 1.0 以降では[アンサー 67308](https://japan.xilinx.com/support/answers/67308.html) の手順に従って VADJ を確認および設定してください。

#### 5.1.1.3. ZCU102 ジャンパーおよびスイッチ
* ブート モードを SD カードに設定します。
  * SW6[4:1]: **オフ、オフ、オフ、オン**
* USB ジャンパーをホスト モードに設定します。USB ジャンパーは、下のボード図で USB コネクタの近くに赤い矩形で示されているエリアにあります。
  * J110: **2-3**
  * J109: **1-2**
  * J112: **2-3**
  * J7: **1-2**
  * J113: **1-2**

  ![](images/zcu102_rv_board_setup_2017.4.jpg)

#### 5.1.1.4. ZCU104 ジャンパーおよびスイッチ
* ブート モードを SD カードに設定します。
  * SW6[4:1]: **オフ、オフ、オフ、オン**

  ![](images/zcu104_board_setup_2017.4.jpg)

### 5.1.2. 8 ストリーム VCU + CNN の設定

#### 5.1.2.1. 必要な操作
* 電源を 12V 電源コネクタに接続します。
* ディスプレイ用に、HDMI ケーブルの一端をボードの HDMI 出力 (上の HDMI コネクタ) に、もう一端をモニターに接続します。
* マイクロ USB ケーブルを USB-UART コネクタに接続します。ターミナル エミュレーターに次の設定を使用します。
  * ボー レート: 115200
  * データ: 8 ビット
  * パリティ: なし
  * ストップ: 1 ビット
  * フロー制御: なし
* `sd_card` ディレクトリからコピーしたビルド済みイメージを含む SD カード (FAT フォーマット) を挿入します。

#### 5.1.2.2. ZCU104 ジャンパーおよびスイッチ
* ブート モードを SD カードに設定します。
  * SW6[4:1]: **オフ、オフ、オフ、オン**

  ![](images/vcu_8stream_cnn.jpg)

## 5.2. デザイン ファイルの抽出

ご使用のシリコン バージョンに対応するリファレンス デザインの ZIP ファイルをダウンロードして解凍します ([ソフトウェア](software-tools-system-requirements.md#32-ソフトウェア)を参照)。
* Linux では、`unzip` ユーティリティを使用します。
* Windows では、リファレンス デザインの ZIP ファイルをスペースを含まないディレクトリ パスに解凍します。7zip ユーティリティを使用して、下の手順に従います。7zip は、[7zip サイト](http://www.7-zip.org/)からダウンロードできます。


**:pushpin: 注記:** ファイルの置換を確認するダイアログ ボックスが表示されたら、**[Auto Rename]** をクリックします (Windows のみ)。

  ![](images/7zip-1.jpg)
<hr/>

:arrow_forward:**次のトピック:** [6. ツール フロー チュートリアル](tool-flow-tutorials.md)

:arrow_backward:**前のトピック:** [4. デザイン ファイルの階層](design-file-hierarchy.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018-2019 Xilinx</sup></p>
