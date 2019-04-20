<p align="right">
            別の言語で表示: <a href="../../Docs/software-tools-system-requirements.md">英語</a>    <table style="width:100%"><table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>reVISION 入門ガイド 2018.3 (UG1265)</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center"><a href="../README.md">1. はじめに</a></td>
    <td width="16%" align="center"><a href="overview.md">2. 概要</a></td>
    <td width="17%" align="center">3. ソフトウェア ツールおよびシステム要件</td>
    <td width="17%" align="center"><a href="design-file-hierarchy.md">4. デザイン ファイルの階層</a></td>
</tr>
<tr>
    <td width="17%" align="center"><a href="operating-instructions.md">5. インストールおよび操作手順</a></td>
    <td width="16%" align="center"><a href="tool-flow-tutorials.md">6. ツール フロー チュートリアル</a></td>
    <td width="17%" align="center"><a href="run-application.md">7. アプリケーションの実行</a></td>
    <td width="17%" align="center"><a href="platform-details.md">8. プラットフォームの詳細</a></td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="known-issues-limitations.md">9. 既知の問題および制限</a></td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. その他のリソース</a></td>
</tr>
</table>

# 3. ソフトウェア ツールおよびシステム要件

## 3.1. ハードウェア

## 3.1.1. シングル センサー プラットフォーム

#### 3.1.1.1. 必須
* [ZCU104 評価ボード](https://japan.xilinx.com/products/boards-and-kits/zcu104.html)または [ZCU102 評価ボード](https://japan.xilinx.com/products/boards-and-kits/ek-u1-zcu102-g.html) (プロダクション シリコンを搭載する rev 1.0)
* マイクロ USB ケーブル、ターミナル エミュレーター用にラップトップまたはデスクトップ コンピューターに接続
* SD カード (ZCU102 の場合) またはマイクロ SD カード (ZCU104 の場合)

#### 3.1.1.2. オプション (ライブ I/O 例には必要)
* 次のいずれかの解像度をサポートする DisplayPort または HDMI 入力を持つモニター:
  * 3840x2160
  * 1920x1080
  * 1280x720
* DisplayPort ケーブル (DP 認証済み) または HDMI ケーブル
* [Leopard LI-IMX274MIPI-FMC](https://leopardimaging.com/product/li-imx274mipi-fmc/)
* [Stereolabs ZED USB ステレオ カメラ](https://zedstore.stereolabs.com/products/zed)
* [e-con Systems See3CAM_CU30_CHL_TC USB カメラ](https://www.e-consystems.com/ar0330-lowlight-usb-cameraboard.asp)
* [USB3 マイクロ B アダプター](http://www.whizzsystems.com/usb3-micro-b-plug-adapter)
  * ZCU102 rev 1.0 およびプロダクション シリコン付属のアダプター。
  * ES2 シリコン搭載の ZCU102 rev 1.0 の場合は、Whizz 社からアダプターを購入する必要があります。
  * ZCU104 ボードにはこのアダプターは不要です。
* 次のいずれかの解像度をサポートする出力を持つ HDMI ビデオ ソース:
  * 3840x2160
  * 1920x1080
  * 1280x720

## 3.1.2. 8 ストリーム VCU + CNN プラットフォーム

**必須:**
* [ZCU104 評価ボード](https://japan.xilinx.com/products/boards-and-kits/zcu104.html)
* マイクロ USB ケーブル、ターミナル エミュレーター用にラップトップまたはデスクトップ コンピューターに接続
* マイクロ SD カード
* 次のいずれかの解像度をサポートする HDMI 入力を持つモニター:
  * 1600x1200
  * 1920x1080
* HDMI ケーブル

## 3.2. ソフトウェア

**必須:**
* ツール フロー チュートリアル実行用にメモリが 32 GB 以上の Linux または Windows ホスト マシン (サポートされる OS バージョンは『SDAccel 開発環境リリース ノート、インストール、およびライセンス ガイド』 ([UG1238](https://japan.xilinx.com/cgi-bin/docs/rdoc?v=2018.3;d=ug1238-sdx-rnil.pdf)) を参照)。
* [SDSoC™ 開発環境](https://japan.xilinx.com/products/design-tools/software-zone/sdsoc.html)バージョン 2018.3 (インストール手順は『SDAccel 開発環境リリース ノート、インストール、およびライセンス ガイド』 ([UG1238](https://japan.xilinx.com/cgi-bin/docs/rdoc?v=2018.3;d=ug1238-sdx-rnil.pdf)) を参照)。
* シリアル ターミナル エミュレーター (Tera Term など)
* デザイン ZIP ファイルを解凍するするための [7zip](http://www.7-zip.org/) ユーティリティ (Windows のみ)。

  **:pushpin: 注意:** ほかの ZIP ユーティリティを使用すると、間違った結果となる可能性があります。

* デザイン ZIP ファイル:
  * シングル センサー ZCU102 プロダクション シリコン: [zcu102-rv-ss-2018-3.zip](https://japan.xilinx.com/member/forms/download/design-license-xef.html?filename=zcu102-rv-ss-2018-3.zip)
  * シングル センサー ZCU104 プロダクション シリコン: [zcu104-rv-ss-2018-3.zip](https://japan.xilinx.com/member/forms/download/design-license-xef.html?filename=zcu104-rv-ss-2018-3.zip)
  * MIN ZCU102 プロダクション シリコン: [zcu102-rv-min-2018-3.zip](https://japan.xilinx.com/member/forms/download/design-license-xef.html?filename=zcu102-rv-min-2018-3.zip)
  * MIN ZCU104 プロダクション シリコン: [zcu104-rv-min-2018-3.zip](https://japan.xilinx.com/member/forms/download/design-license-xef.html?filename=zcu104-rv-min-2018-3.zip)
  * 8 ストリーム VCU + CNN ZCU104 プロダクション シリコン用のデザイン ZIP ファイルはまだ提供されていません。

## 3.3. ライセンス

  **:pushpin: 重要:** このリファレンス デザインの一部は、サードパーティにより別途ライセンス付与されるもので、GNU 一般公衆利用許諾書バージョン 2、GNU 劣等一般公衆利用許諾書バージョン 2.1 などのライセンスに基づいています。[サードパーティ ライブラリ ソース](https://japan.xilinx.com/member/forms/download/design-license-xef.html?filename=zcu10x-rv-ss-2018-3-tpl-sources.zip) ファイルに、リファレンス デザインに含まれていない別途にライセンス付与されるもののコピーが含まれます。

このデザインをビルドするには、SDSoC ライセンスのみが必要です。[このサイト](https://japan.xilinx.com/products/design-tools/software-zone/sdsoc.html#buy)から 60 日間有効な評価版を入手するか、ツールを購入できます。

### 3.3.1. ライセンスの生成手順
1. [ライセンス サイト](https://japan.xilinx.com/getproduct)にログインします。アカウントがない場合は、[アカウントを作成] リンクをクリックしてアカウントを作成してください。
1. [Create New Licenses] タブで **[SDSoC Environment, 60 Day Evaluation License]** のチェック ボックスをオンにし、[Generate] ボタンをクリックしてライセンスを生成します。

   ![](images/license.png)

1. システム情報の下にホストの詳細を入力します。
1. 使用許諾契約まで進み、承認します。
1. ライセンス ファイル (`.lic`) がアカウントに設定されている電子メールに送付されます。
1. ライセンス ファイルをローカルにコピーし、SDSoC License Manager にそのパスを入力します。

## 3.4. 互換性

リファレンス デザインは、次のコンポーネントを使用してテストされています。

**モニター:**

| **メーカー/モデル** | **ネイティブ解像度** |
|----|----|
| Viewsonic VP2780-4K | 3840x2160 |
| Acer S277HK | 3840x2160 |
| Dell U2414H | 1920x1080 |


**HDMI ソース:**

| **メーカー/モデル** | **解像度** |
|----|----|
| Nvidia Shield TV | 3840x2160、1920x1080 |
| OTT TV BOX M8N | 3840x2160、1920x1080、1280x720 |
| Roku 2 XS | 1920x1080、1280x720 |
| TVix Slim S1 Multimedia Player | 1920x1080、1280x720 |


**USB3 カメラ:**

| **メーカー/モデル** | **解像度** |
|----|----|
| ZED ステレオ カメラ | 3840x1080、2560x720 |
| See3CAM_CU30 | 1920x1080、1280x720 |


**DisplayPort ケーブル:**
* Cable Matters DisplayPort Cable-E342987
* Monster Advanced DisplayPort Cable-E194698



<hr/>

:arrow_forward:**次のトピック:** [4. デザイン ファイルの階層](design-file-hierarchy.md)

:arrow_backward:**前のトピック:** [2. 概要](overview.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018-2019 Xilinx</sup></p>
