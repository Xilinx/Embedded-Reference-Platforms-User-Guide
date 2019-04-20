<p align="right">
            別の言語で表示: <a href="../../Docs/design-file-hierarchy.md">英語</a>    <table style="width:100%"><table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>reVISION 入門ガイド 2018.3 (UG1265)</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center"><a href="../README.md">1. はじめに</a></td>
    <td width="16%" align="center"><a href="overview.md">2. 概要</a></td>
    <td width="17%" align="center"><a href="software-tools-system-requirements.md">3. ソフトウェア ツールおよびシステム要件</a></td>
    <td width="17%" align="center">4. デザイン ファイルの階層</td>
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

# 4. デザイン ファイルの階層

Zynq® UltraScale+™ MPSoC reVISION プラットフォームの ZIP ファイルには、SDx™ 環境でプロジェクトを作成してサンプル アプリケーションをビルドするために必要なバイナリおよびソース ファイルが含まれています。サンプル アプリケーションは、実行するテスト デザインを含む GStreamer プラグインとしてビルドされます。


シングル センサー プラットフォームには、5 つのファイル I/O 例と 4 つのライブ I/O 例が含まれています。ファイル I/O 例は入力画像ファイルを読み込んで出力画像ファイルを生成し、ライブ I/O 例はビデオ ソースからビデオ入力を読み込んでディスプレイにライブ ビデオを出力します。シングル センサー reVISION プラットフォームには、次のコンポーネントが含まれます。

* `zcu102_rv_ss` SDSoC プラットフォーム
  * `hw`: ハードウェア プラットフォームを記述する .dsa ファイルが含まれます。
  * `samples`: サンプル アプリケーション コードが含まれます。各サンプル ディレクトリには、ビルド プロセスを記述する .json ファイルが含まれます。これらは、reVISION プラットフォームを使用して新しいプロジェクトを作成するときに [Template] ダイアログ ボックスに表示される SDx サンプル アプリケーションです。
    * `file_IO` プロジェクトは自己完結型です。
    * `live_IO` プロジェクトはより複雑で、複数の手順でビルドされます。<a href="run-application.md">アプリケーションの実行</a>を参照してください。
  * `sw`: ZCU10x ターゲット ボード上のプロセッサ用のソフトウェア、ブートローダー、およびその他のコードとサポート ファイルが含まれます。
* `petalinux`: デバイス ツリー情報、ハードウェア記述ファイル、その他のシステム セットアップ ファイルを含む PetaLinux BSP が含まれます。上級ユーザーは、独自のプラットフォームを作成するオプションもあります。
* `sd_card`: ZCU10x ボードでライブ I/O 例アプリケーションを実行できるようにするビルド済み SD カード イメージが含まれます。
* `workspaces`: `live_IO` サンプルをビルドするのに使用可能なワークスペース ディレクトリ構造が含まれます。<a href="run-application.md">アプリケーションの実行</a>を参照してください。

```
zcu102-rv-ss-2018-3
├── IMPORTANT_NOTICE_CONCERNING_THIRD_PARTY_CONTENT.txt
├── petalinux
│   ├── sdk.sh
│   └── zcu102-prod-rv-ss.bsp
├── README.txt
├── sd_card
│   ├── filter2d
│   ├── optical_flow
│   ├── stereo
│   └── triple
├── workspaces
│   ├── ws_f2d
│   │   ├── gst
│   │   │   ├── apps
│   │   │   └── plugins
│   │   └── scripts
│   ├── ws_of
│   │   ├── gst
│   │   │   ├── apps
│   │   │   └── plugins
│   │   └── scripts
│   ├── ws_sv
│   │   ├── gst
│   │   │   ├── apps
│   │   │   └── plugins
│   │   └── scripts
│   └── ws_triple
│       ├── gst
│       └── scripts
└── zcu102_rv_ss
    ├── hw
    │   └── zcu102_rv_ss.dsa
    ├── samples
    │   ├── file_IO
    │   │   ├── bilateral_fileio
    │   │   ├── harris_fileio
    │   │   ├── opticalflow_fileio
    │   │   ├── steoreolbm_fileio
    │   │   └── warptransform_fileio
    │   └── live_IO
    │       ├── filter2d
    │       ├── optical_flow
    │       ├── stereo
    │       └── triple
    ├── sw
    │   ├── a53_linux
    │   │   ├── a53_linux
    │   │   └── boot
    │   ├── prebuilt
    │   └── zcu102_rv_ss.spfm
    └── zcu102_rv_ss.xpfm
```

MIN reVISION プラットフォームには、次のコンポーネントが含まれます。

* `zcu102_rv_min` SDSoC プラットフォーム
  * `hw`: ハードウェア プラットフォームを記述する .dsa ファイルが含まれます。
  * `sw`: ZCU10x ターゲット ボード上のプロセッサ用のソフトウェア、ブートローダー、およびその他のコードとサポート ファイルが含まれます。
* `petalinux`: デバイス ツリー情報、ハードウェア記述ファイル、その他のシステム セットアップ ファイルを含む PetaLinux BSP が含まれます。上級ユーザーは、独自のプラットフォームを作成するオプションもあります。


```
zcu102-rv-min-2018-3
├── IMPORTANT_NOTICE_CONCERNING_THIRD_PARTY_CONTENT.txt
├── README.txt
└── zcu102_rv_min
    ├── hw
    │   └── zcu102_rv_min.dsa
    ├── petalinux
    │   ├── sdk.sh
    │   └── zcu102-prod-rv-min.bsp
    ├── samples
    ├── sw
    │   ├── a53_linux
    │   │   ├── a53_linux
    │   │   └── boot
    │   ├── prebuilt
    │   └── zcu102_rv_min.spfm
    └── zcu102_rv_min.xpfm
```

8 ストリーム VCU + CNN reVISION プラットフォームには、次のコンポーネントが含まれます。
* `zcu104` SDSoC プラットフォーム
  * `hw`: ハードウェア プラットフォームを記述する .dsa ファイルが含まれます。
  * `sw`: ZCU104 ターゲット ボード上のプロセッサ用のソフトウェア、ブートローダー、およびその他のコードとサポート ファイルが含まれます。
* `petalinux`: デバイス ツリー情報、ハードウェア記述ファイル、その他のシステム セットアップ ファイルを含む PetaLinux BSP が含まれます。上級ユーザーは、独自のプラットフォームを作成するオプションもあります。
* `SDcard`: 8 ストリーム VCU + CNN デモを実行できるようにするビルド済み SD カード イメージが含まれます。
* `scripts`: 8 ストリーム VCU + CNN デモを実行するためのテスト スクリプトが含まれます。これらのスクリプトは `SDcard` にも含まれます。

```
zcu104-rv-vcu-ml-2018-3
├── IMPORTANT_NOTICE_CONCERNING_THIRD_PARTY_CONTENT.txt
├── petalinux
│   ├── sdk.sh
│   └── zcu104_vcu_ml.bsp
├── README.txt
├── scripts
│   ├── demo_8_streams_1080.sh
│   └── demo_8_streams_4k.sh
├── SDcard
└── zcu104
    ├── hw
    │   └── zcu104.dsa
    ├── samples
    ├── sw
    │   ├── a53_linux
    │   │   ├── a53_linux
    │   │   └── boot
    │   ├── prebuilt
    │   └── zcu104.spfm
    └── zcu104.xpfm
```
<hr/>

:arrow_forward:**次のトピック:** [5. インストールおよび操作手順](operating-instructions.md)

:arrow_backward:**前のトピック:** [3. ソフトウェア ツールおよびシステム要件](software-tools-system-requirements.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018-2019 Xilinx</sup></p>
