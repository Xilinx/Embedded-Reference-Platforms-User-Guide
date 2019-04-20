<p align="right">
            別の言語で表示: <a href="../../Docs/run-application.md">英語</a>    <table style="width:100%"><table style="width:100%">
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
    <td width="17%" align="center"><a href="operating-instructions.md">5. インストールおよび操作手順</a></td>
    <td width="16%" align="center"><a href="tool-flow-tutorials.md">6. ツール フロー チュートリアル</a></td>
    <td width="17%" align="center">7. アプリケーションの実行</td>
    <td width="17%" align="center"><a href="platform-details.md">8. プラットフォームの詳細</a></td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="known-issues-limitations.md">9. 既知の問題および制限</a></td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. その他のリソース</a></td>
</tr>
</table>

# 7. アプリケーションの実行

GStreamer プラグインを使用するには、それを含むビデオ パイプラインをセットアップして起動する必要があります。これには、コマンド ライン ユーティリティ `gst-launch-1.0` を使用できます。シリアル ターミナル エミュレーターを使用してターゲット ボードに接続しているラップトップを使用して、標準 Linux コンソール セッションによってシステムと通信します。[ライブ I/O オプティカル フロー サンプル アプリケーションのビルド](tool-flow-tutorials.md#611-ライブ-io-オプティカル-フロー-サンプル-アプリケーションのビルド)を参照してください。1 つまたは複数のソース、0 個以上のアクセラレータ、および 1 つのシンクを含むビデオ パイプライン グラフを構築できます。GStreamer は、キャプチャ、M2M (Memory-to-Memory)、およびディスプレイ パイプラインを初期化し、パイプライン段を通過するビデオ バッファー フローを制御します。

``gst-launch`` ユーティリティは、デバッグ ツールです。プラグインをセットアップして起動するには、GStreamer ライブラリへの API 呼び出しを使用してパイプラインをセットアップして実行するコンパイル済みのアプリケーションを使用する方法もあります。これを実行するためのテスト アプリケーション用のサンプルのコードが提供されています。各ライブ I/O サンプルのシングル センサー プラットフォームの `./gst/apps/<name>` フォルダーを確認してください。


## 7.1. ライブ I/O サンプル アプリケーションの実行 (シングル センサー プラットフォーム)

ハードウェア アクセラレーションされたコードを含む bottom プロジェクトは SDx™ 環境プロジェクト (`./ws_f2d/filter2d` など) です。完了すると SD カード イメージが作成されるので、そこに含まれるファイルをターゲット ボードで使用する SD カードにコピーします。すべてのライブラリおよびプラグインを ``sd_card`` のルート ディレクトリにコピーする必要があります。次のセクションに、各サンプル アプリケーションのファイルを示します。

:pushpin: **重要:** stereo および triple の場合は、SD カードにカメラ設定ファイルも必要です。[シングル センサー プラットフォーム ステレオ デモ: 特別な考慮事項](#74-シングル-センサー-プラットフォーム-ステレオ-デモ-特別な考慮事項)を参照してください。

### 7.1.1. filter2d のファイル

bottom ライブラリをビルドすると、``sd_card`` ディレクトリに次のファイルが含まれます。
* `./ws_f2d/filter2d/Release/sd_card/image.ub`
* `./ws_f2d/filter2d/Release/sd_card/BOOT.BIN`
* `./ws_f2d/filter2d/Release/sd_card/libfilter2d.so`

top プロジェクトは、共有ライブラリとデモ アプリケーションを生成します。
* `./ws_f2d/gst/plugins/filter2d/Debug/libgstsdxfilter2d.so`
* `./ws_f2d/gst/apps/filter2d/Debug/gstdemo.`

>**:information_source: ヒント:** すべてのイメージを SD カードのルートに直接コピーしてください。

### 7.1.2. opticalflow のファイル

bottom ライブラリをビルドすると、``sd_card`` ディレクトリに次のファイルが含まれます。
* `./ws_of/opticalflow/Release/sd_card/image.ub`
* `./ws_of/opticalflow/Release/sd_card/BOOT.BIN`
* `./ws_of/opticalflow/Release/sd_card/libopticalflow.so`

top プロジェクトは、共有ライブラリとデモ アプリケーションを生成します。
* `./ws_of/gst/plugins/optical_flow/Debug/libgstsdxopticalflow.so`
* `./ws_of/gst/apps/optical_flow/Debug/gstdemo.`

>**:information_source: ヒント:** すべてのイメージを SD カードのルートに直接コピーしてください。

### 7.1.3. stereo のファイル

bottom ライブラリをビルドすると、``sd_card`` ディレクトリに次のファイルが含まれます。
* `./ws_sv/stereo/Release/sd_card/image.ub`
* `./ws_sv/stereo/Release/sd_card/BOOT.BIN`
* `./ws_sv/stereo/Release/sd_card/libstereo.so`

top プロジェクトは、共有ライブラリとデモ アプリケーションを生成します。
* `./ws_sv/gst/plugins/stereo/Debug/libgstsdxstereo.so`
* `./ws_sv/gst/apps/stereo/Debug/gstdemo.`

>**:information_source: ヒント:** すべてのイメージを SD カードのルートに直接コピーしてください。

### 7.1.4. triple のファイル

bottom ライブラリをビルドすると、``sd_card`` ディレクトリに次のファイルが含まれます。
* `./ws_triple/triple/Release/sd_card/image.ub`
* `./ws_triple/triple/Release/sd_card/BOOT.BIN`
* `./ws_triple/triple/Release/sd_card/libtriple.so`

top プロジェクトは、共有ライブラリとデモ アプリケーションを生成します。
* `./ws_triple/gst/plugins/filter2d/Debug/libgstsdxfilter2d.so`
* `./ws_triple/gst/plugins/optical_flow/Debug/libgstsdxopticalflow.so`
* `./ws_triple/gst/plugins/stereo/Debug/libgstsdxstereo.so`
* `./ws_triple/gst/apps/triple/Debug/gstdemo.`

>**:information_source: ヒント:** すべてのイメージを SD カードのルートに直接コピーしてください。

### 7.1.5. 手順

1. ターゲット ボードの SD カード スロットに SD カードを挿入します。
2. ボードの電源をオンにします。数秒後に INIT_B LED とその横にある DONE LED が緑色になることを確認してください。
3. コンピューターからシステムを制御します。TeraTerm、PuTTY などを使用してシリアル ターミナル セッションを開始します。[ライブ I/O オプティカル フロー サンプル アプリケーションのビルド](tool-flow-tutorials.md#611-ライブ-io-オプティカル-フロー-サンプル-アプリケーションのビルド)を参照してください。USB-UART ケーブルが接続され、ボードの電源がオンの状態なので、応答している COM ポートを見つけることができます。Linux ブートストラップおよびデバッグ メッセージが数ページ分表示され、最後に Linux コマンド ライン プロンプトが表示されます。
4. ``cd`` コマンドを使用して `/media/card` ディレクトリに移動します。このディレクトリには、SD カードにコピーしたすべてのファイルが含まれます。
```
# cd /media/card

```
5. 共有ライブラリを適切な場所にコピーします。該当する例を参照してください。

**:pushpin: 注記:** reVISION BSP/イメージを使用する場合は、``PATH`` 環境変数に ``/media/card/`` が追加されるので、次の手順は不要です。

  * filter2d の場合:

	```
	# cp libfilter2d.so /usr/lib
	# cp libgstsdxfilter2d.so /usr/lib/gstreamer-1.0

	```
  * opticalflow の場合:

	```
	# cp libopticalflow.so /usr/lib
	# cp libgstsdxopticalflow.so /usr/lib/gstreamer-1.0

	```

  * stereo の場合:
	```

	# cp libstereo.so /usr/lib
	# cp libgstsdxstereo.so /usr/lib/gstreamer-1.0

	```

  * triple の場合:
	```

	# cp libtriple.so /usr/lib
	# cp libgstsdxfilter2d.so /usr/lib/gstreamer-1.0
	# cp libgstsdxopticalflow.so /usr/lib/gstreamer-1.0
	# cp libgstsdxstereo.so /usr/lib/gstreamer-1.0

	```


### 7.1.6. GStreamer アプリケーション

gstreamer パイプラインを作成して実行するには、ソースからコンパイルされた ``gst`` デモ アプリケーションを使用するか、ビルド済みの `gst-launch` ユーティリティを使用します。コンパイル済みのデモ プログラムを使用するには、次のコマンドを実行します。
```

# ./gstdemo

```

  * デモ プログラムはすべて、ミキサーを介して HDMI 出力を使用します。
  * filter2d デモは HDMI 入力を使用します。
  * opticalflow デモは MIPI 入力を使用します。
  * stereo デモは USB ZED ステレオ カメラ入力を使用します。
  * triple のデモは上記すべての入力を使用します。

次のコード例は、1920x1080、YUY2 の MIPI からミキサー プレーン 29 を介する HDMI 出力への ``filter2d`` パイプラインを実行する ``gst-launch`` コマンドです。
```

gst-launch-1.0 \
    xlnxvideosrc src-type="mipi" ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxfilter2d filter-preset=4 filter-mode=1 ! queue ! \
    xlnxvideosink sink-type="hdmi" plane-id=29 sync=false fullscreen-overlay=true

```

次のコード例は、1920x1080、YUY2 の HDMI からミキサー プレーン 29 を介する HDMI 出力への ``opticalflow`` パイプラインを実行する ``gst-launch`` コマンドです。
```

gst-launch-1.0 \
    xlnxvideosrc src-type="hdmi" ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxopticalflow filter-mode=1 ! queue ! \
    xlnxvideosink sink-type="hdmi" sync=false fullscreen-overlay=true

```


次のコード例は、3840x1080 の隣り合わせの入力、YUY2 の USB からミキサー プレーン 29 を介した HDMI の 1920x1080 出力へのステレオ パイプラインを実行する ``gst-launch`` コマンドです。``config-filename`` プロパティをご使用のカメラのシリアル番号に置き換える必要があります。[シングル センサー プラットフォーム ステレオ デモ: 特別な考慮事項](#74-シングル-センサー-プラットフォーム-ステレオ-デモ-特別な考慮事項)を参照してください。
```

gst-launch-1.0 \
    xlnxvideosrc src-type="usbcam"  ! \
    "video/x-raw, width=3840, height=1080, format=YUY2" ! \
    sdxstereo filter-mode=1 config-filename=/media/card/SN12263.conf ! queue ! \
    xlnxvideosink sink-type="hdmi" plane-id=29 sync=false fullscreen-overlay=true

```


次の例は、秒ごとのフレーム数ディスプレイをイネーブルにして ``filter2d`` を実行する別の方法を示しています。出力パイプ段は ``fpsdisplaysink`` で、先ほど使用した ``xlnxvideosink....`` 文字列は ``video-sink`` という ``fpsdisplaysink`` プロパティの 1 つです。
```

gst-launch-1.0 \
    xlnxvideosrc src-type="mipi" ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxfilter2d filter-preset=4 filter-mode=1 ! queue ! \
    fpsdisplaysink video-sink="xlnxvideosink sink-type=hdmi plane-id=29 fullscreen-overlay=true" sync=false text-overlay=false -v

```
## 7.2. 交通量検出サンプル アプリケーションの実行 (8 ストリーム VCU + CNN プラットフォーム)

ハードウェア アクセラレーションされたコードを含む C 呼び出し可能プロジェクトは、SDx™ 環境プロジェクト (`./ws_dpu/dpu130_4096` など) です。完了すると SD カード イメージが作成されるので、そこに含まれるファイルをターゲット ボードで使用する SD カードにコピーします。すべてのライブラリおよびプラグインを ``sd_card`` のルート ディレクトリにコピーする必要があります。次のセクションに、各サンプル アプリケーションのファイルを示します。

### 7.2.1. 交通量検出のファイル

C 呼び出し可能ライブラリをビルドすると、``sd_card`` ディレクトリに次のファイルが含まれます。
* `./ws_dpu/dpucore130_4096/Debug/sd_card/image.ub`
* `./ws_dpu/dpucore130_4096/Debug/sd_card/uENV.txt`
* `./ws_dpu/dpucore130_4096/Debug/sd_card/BOOT.BIN`
* `./ws_dpu/dpucore130_4096/Debug/sd_card/libdpucore130_4096.so`

  **:pushpin: 注記:** ``libdpucore130_4096.so`` を使用する場合は、``libdpucore.so`` という名前に変更するか、これをポイントするソフト リンクを作成してください。

``gstsdxtrafficdetect`` プロジェクトは、共有ライブラリを生成します。
* `./ws_dpu/gstsdxtrafficdetect/Debug/libgstsdxtrafficdetect.so`

ビルド済みライブラリを追加します。
* `./run_dpu/lib/libn2cube.so`
* `./run_dpu/lib/libdputils.so`
* `./run_dpu/libmodel/libdpumodelssd.so`

>**:information_source: ヒント:** すべてのイメージを SD カードのルートに直接コピーしてください。

### 7.2.2. 手順

1. ターゲット ボードの SD カード スロットに SD カードを挿入します。
2. ボードの電源をオンにします。数秒後に INIT_B LED とその横にある DONE LED が緑色になることを確認してください。
3. コンピューターからシステムを制御します。TeraTerm、PuTTY などを使用してシリアル ターミナル セッションを開始します。[ライブ I/O オプティカル フロー サンプル アプリケーションのビルド](tool-flow-tutorials.md#611-ライブ-io-オプティカル-フロー-サンプル-アプリケーションのビルド)を参照してください。USB-UART ケーブルが接続され、ボードの電源がオンの状態なので、応答している COM ポートを見つけることができます。Linux ブートストラップおよびデバッグ メッセージが数ページ分表示され、最後に Linux コマンド ライン プロンプトが表示されます。
4. ``cd`` コマンドを使用して `/media/card` ディレクトリに移動します。このディレクトリには、SD カードにコピーしたすべてのファイルが含まれます。
```
# cd /media/card

```
5. 共有ライブラリを適切な場所にコピーします。

**:pushpin: 注記:** reVISION BSP/イメージを使用する場合は、``PATH`` 環境変数に ``/media/card/`` が追加されるので、次の手順は不要です。


```
# cp libdpucore.so /usr/lib
# cp libn2cube.so /usr/lib
# cp libdputils.so /usr/lib
# cp libdpumodelssd.so /usr/lib
# cp libgstsdxtrafficdetect.so /usr/lib/gstreamer-1.0

```
### 7.2.3. 例

次のコード例は、既に ``demo_input`` フォルダーにある H264 エンコード ファイルからの入力とミキサー プレーン 29 を介した HDMI 出力を使用して、``gst-launch`` コマンドでシングル ストリーム VCU + CNN パイプラインを実行します。
```

  gst-launch-1.0 multifilesrc location=demo_inputs/file_%02d.dmp loop=true ! h264parse !          omxh264dec internal-entropy-buffers=3 ! xlnxscale need-tdm=true !  \
  video/x-raw, width=480, height=360, format=BGR !  \
          sdxtrafficdetect ! queue ! \
          fpsdisplaysink video-sink="kmssink plane-id=29 bus-id="a0070000.v_mix" render-rectangle=\"<0,0,480,360>\"" text-overlay=false sync=false -v


```

8 ストリーム プラットフォームでは、8 つの類似のインスタンスを 29 ～ 36 の番号が付いた ``plane-id`` の異なるミキサーで実行できます。完成したパイプラインは `demo_8_streams_4k.sh` を確認してください。解像度が 1600x1200 のモニターがある場合は、次の例のようにスクリプトを実行します。
```
  source demo_8_streams_4k.sh
```
ご使用のモニターで解像度 1600x1200 がサポートされない場合は、次の例のようにスクリプトを実行します。
```
source demo_8_streams_1080.sh
```

``demo_input`` フォルダーには H264 エンコードのトラフィック ビデオ ファイルが含まれます。これらのファイルは、DDR の使用量を最小限に抑えるため、Gstreamer プラグイン ``multifilesink`` により小さく分割されます。

```
gst-launch-1.0 filesrc location=<input_largefile.264> ! multifilesink location="file%d.dmp" next-file=4 max-file-size=<keep based on current input fragmented file>
```

上記の分割は実際には必要ありません。ファイルを、次の例に示すように ``filesrc`` を使用して完成させることもできます。
```

  gst-launch-1.0 filesrc location=<testfile.h264> ! h264parse ! omxh264dec internal-entropy-buffers=3 ! xlnxscale need-tdm=true !  \
  video/x-raw, width=480, height=360, format=BGR !  \
          sdxtrafficdetect ! queue ! \
          fpsdisplaysink video-sink="kmssink plane-id=29 bus-id="a0070000.v_mix" render-rectangle=\"<0,0,480,360>\"" text-overlay=false sync=false -v
```


## 7.3. Gstreamer エレメント

これらのパイプラインでは、``xlnxvideosrc``、``queue``、``xlnxvideosink``、および ``sdxfilter2d`` (あるいは ``sdxopticalflow`` または ``sdxstereo``) エレメントが使用されます。Gstreamer ユーティリティ ``gst-inspect-1.0`` を使用すると、これらのエレメントのプロパティおよびその他詳細情報を表示できます。

### 7.3.1. xlnxvideosrc

```

# gst-inspect-1.0 xlnxvideosrc

```

  * ``src-type`` プロパティ
    - (-1): none: ビデオ ソースなし
    - (0): vivid: 仮想ビデオ デバイス
    - (1): mipi: MIPI CSI2 RX
    - (2): hdmi: HDMI 入力
    - (3): usbcam: USB ウェブキャム
    - (4): tpg: テスト パターン ジェネレーター
    - (5): mipi_quad_vc0: MIPI クワッド仮想チャネル 0
    - (6): mipi_quad_vc1: MIPI クワッド仮想チャネル 1
    - (7): mipi_quad_vc2: MIPI クワッド仮想チャネル 2
    - (8): mipi_quad_vc3: MIPI クワッド仮想チャネル 3

  * 子:
    - ``v4l2src0``



### 7.3.2. キュー

これは必須ではありませんが、使用するとフレーム レートが高くなるので、パフォーマンスが向上します。

### 7.3.3. xlnxvideosink

xlnxvideosink プラグインを調べるには、次のコマンドを使用します。
```

gst-inspect-1.0 xlnxvideosink

```

* ``sink-type`` プロパティ
  * (-1): none: なし。
  * (0): dp: DisplayPort。
  * (1): hdmi: HDMI 出力。

* ``plane-id`` プロパティ
  * ``b00c0000.v_mix`` (HDMI 出力) を使用する場合:
    - ``29`` は YUY2 プレーンです。
    - ``30`` は YUY2 プレーンです。
    - ``31`` は UYUV プレーンです。
* ``fd4a0000.zynqmp-display`` (DP 出力) を使用する場合:
    - ``35`` は RGB をサポートします。
    - ``34`` は YUY2 および UYVY をサポートします。
* 子:
  - ``kmssink0``

### 7.3.4. xlnxscale

  ``xlnxscale`` プラグインを調べるには、次のコマンドを使用します。
  ```

  # gst-inspect-1.0 xlnxscale

  ```

  * ``need-tdm`` プロパティ
    * "true": 時分割多重化 (TDM) をイネーブルにします。
    "false": 時分割多重化 (TDM) をディスエーブルにします。

### 7.3.5. sdx&lt;accelerator&gt;

``sdxfilter2d`` プラグインを調べるには、次のコマンドを使用します。
```

# gst-inspect-1.0 sdxfilter2d

```

* ``filter_mode`` プロパティ
  * 1: ハードウェア アクセラレーションを使用します。
  * 0: ソフトウェアを使用します (filter2d コードは完全に Arm™ プロセッサ上で実行)。
* ``filter_preset`` プロパティ
  * プリセット フィルターを 1 ～ 10 から選択します。例では 4 に設定しており、エッジ強調フィルター (emboss) を使用しています。
* ``coefficients`` プロパティ
  * 3x3 係数マトリックスの配列です (例: `coefficients="<<0,0,0>,<0,-1,0>,<0,0,0>>"`)。

``sdxopticalflow`` プラグインを調べるには、次のコマンドを使用します。
```

# gst-inspect-1.0 sdxopticalflow

```

* ``filter_mode`` プロパティ
  * 1: ハードウェア アクセラレーションを使用します。
  * 0: ソフトウェアを使用します (オプティカル フロー コードを完全に Arm プロセッサ上で実行)。

``sdxstereo`` プラグインを調べるには、次のコマンドを使用します。
```

# gst-inspect-1.0 sdxstereo

```

* ``filter_mode`` プロパティ
  * 1: ハードウェア アクセラレーションを使用します。
  * 0: ソフトウェアを使用します (オプティカル フロー コードは完全に Arm プロセッサ上で実行)。
* ``config-filename`` プロパティ
  * これで ZED カメラ設定ファイルを指定します。カメラ設定ファイルは、SD カードに含めておく必要があります。[シングル センサー プラットフォーム ステレオ デモ: 特別な考慮事項](#74-シングル-センサー-プラットフォーム-ステレオ-デモ-特別な考慮事項)を参照してください。

## 7.4. シングル センサー プラットフォーム ステレオ デモ: 特別な考慮事項

ステレオ ビジョン デモは、複数の点から特別です。まず、USB ビデオ入力に接続されている ZED ステレオ カメラを使用する必要があります。次に、このアプリケーションに限り、入力画像解像度の幅が出力解像度の幅の 2 倍になっています。入力は 2 つの並んだ画像で構成されており、同期化された左および右ステレオ入力がカメラから供給されます。2560x720 を入力して 1280x720 を出力、3840x1080 を入力して 1920x1080 を出力する 2 つのモードが可能です。デフォルトの 3840x2160 出力解像度はステレオ ビジョン アプリケーションではサポートされていません。

もう 1 つの注意点は、システムに接続されているカメラに対応する設定ファイルを使用する必要があるということです。各 StereoLabs ZED カメラには、特有のパラメーター ファイルが関連付けられています。このテキスト ファイルは StereoLabs から提供されているもので、ステレオ ビジョン デモを正しく機能させるためには、SD カードに存在する必要があります。特定のカメラ用のファイルは、シリアル番号 (ZED カメラの箱および ZED カメラの USB プラグの近くにある黒いタグに記載) から特定できます。シリアル番号は S/N 000012345 という形式であり、このカメラに対応するパラメーター ファイルは ``SN12345.conf`` という名前です。パラメーター ファイルをダウンロードするには、http://calib.stereolabs.com/?SN=XXXXX (XXXXX を実際のシリアル番号に置換) にアクセスします。これにより、設定ファイルをコンピューターにダウンロードできます。

ステレオ ブロック マッチング アルゴリズムでは、人間が深度を認識するのと同様の方法である両眼視差に基づいて深度を計算します。深度マップは、擬色でコード記述されます。遠い物体は濃い青で示されます。物体が近くなるほど徐々に緑、黄、オレンジ、赤、紫と変化していき、最終的に 720p の場合はカメラから 2 フィート、1080p の場合はカメラから 5 フィートの距離にある物体が白で示されます。これより近い物体、および画像でテクスチャのない滑らかな領域は追跡できず、黒で表示されます。細部情報の多い (特に垂直エッジが多い) 部分が最も良く追跡できます。左側の大きな領域 (128 ピクセル幅) が黒であるのは普通で、これは双眼鏡の右と左の画像間でベスト マッチを水平検索するための領域を表します。



<hr/>

:arrow_forward:**次のトピック:** [8. プラットフォームの詳細](platform-details.md)

:arrow_backward:**前のトピック:** [6. ツール フロー チュートリアル](tool-flow-tutorials.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018-2019 Xilinx</sup></p>
