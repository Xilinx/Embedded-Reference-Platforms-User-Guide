<p align="right">
            別の言語で表示: <a href="../run-application.md">英語</a>    <table style="width:100%"><table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>reVISION 入門ガイド 2018.2</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center"><a href="README.md">1. はじめに</a></td>
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

# 7 アプリケーションの実行

GStreamer プラグインを使用するには、それを含むビデオ パイプラインをセットアップして起動する必要があります。これには、コマンド ライン ユーティリティ `gst-launch-1.0` を使用できます。シリアル ターミナル エミュレーターを介してターゲット ボードに接続しているラップトップを使用して、標準 Linux コンソール セッションによってシステムと通信します。[セクション 6.1](tool-flow-tutorials.md#61-live_io-オプティカル-フロー-サンプル-アプリケーションのビルド) を参照してください。1 つまたは複数のソース、0 個以上のアクセラレータ、および 1 つのシンクを含むビデオ パイプライン グラフを構築できます。GStreamer は、キャプチャ、M2M (Memory-to-Memory)、およびディスプレイ パイプラインを初期化し、パイプライン段を通過するビデオ バッファー フローを制御します。

gst-launch ユーティリティは、デバッグ ツールです。プラグインをセットアップして起動するには、GStreamer ライブラリへの API 呼び出しを使用してパイプラインをセットアップして実行するコンパイル済みのアプリケーションを使用する方法もあります。これを実行するためのテスト アプリケーション用のサンプルのコードが提供されています。各 live_IO サンプルの `./gst/apps/<name>` フォルダーを確認してください。

HDMI および MIPI 入力チャネルは、それ自体が設定する必要のあるハードウェア パイプラインです。このタスクは `video_cmd` ユーティリティにより実行され、ビデオ入力を使用するパイプラインを開始する前に一度実行します。`video_cmd` ユーティリティは、sd_card ディレクトリにあります。これは、MIPI または HDMI 入力チャネルを使用する場合にのみ必要です。

## 7.1 live_IO I/O サンプル アプリケーションの実行

* ハードウェア アクセラレーションされたコードを含む bottom プロジェクトは SDx プロジェクト (`./ws_f2d/filter2d` など) です。完了すると sd_card イメージが作成されるので、そこに含まれるファイルをターゲット ボードで使用する SD カードにコピーします。
* sd_card ディレクトリを SD カードにコピーする際、SD カード内に lib と gstreamer-1.0 という名前の 2 つのディレクトリを作成してください。
* ライブラリはすべて lib ディレクトリに、サンプル プラグインは gstreamer-1.0 にコピーして、残りのイメージは sd_card ルート ディレクトリにコピーします。
* 次のセクションに、各サンプル アプリケーションのファイルを示します。
* stereo および triple には、stereo が含まれるので、sd_card にカメラ コンフィギュレーション ファイルも必要です。下の[ステレオ デモの詳細](#73-ステレオ-デモの詳細)を参照してください。

**filter2d の場合**

bottom ライブラリをビルドすると、sd_card ディレクトリに次のファイルが含まれます。
* `./ws_f2d/filter2d/Release/sd_card/image.ub`
* `./ws_f2d/filter2d/Release/sd_card/BOOT.BIN`
* `./ws_f2d/filter2d/Release/sd_card/libfilter2d.so`
* `./ws_f2d/filter2d/Release/sd_card/video_cmd`


top プロジェクトは、共有ライブラリとデモ アプリケーションを生成します。
* `./ws_f2d/gst/plugins/filter2d/Debug/libgstsdxfilter2d.so`
* `./ws_f2d/gst/base/Debug/libgstsdxbase.so`
* `./ws_f2d/gst/allocators/Debug/libgstsdxallocator.so`
* `./ws_f2d/gst/apps/filter2d/Debug/gstdemo.`

>**:information_source: ヒント:**
> * libfilter2d.so、libgstsdxbase.so、および libgstsdxallocator.so を lib ディレクトリにコピーします。
> * libgstsdxfilter2d.so を gstreamer-1.0 にコピーします。
> * 残りすべてのイメージを SD カードのルート フォルダーにコピーします。

**opticalflow の場合**

bottom ライブラリをビルドすると、sd_card ディレクトリに次のファイルが含まれます。
* `./ws_of/opticalflow/Release/sd_card/image.ub`
* `./ws_of/opticalflow/Release/sd_card/BOOT.BIN`
* `./ws_of/opticalflow/Release/sd_card/libopticalflow.so`
* `./ws_of/opticalflow/Release/sd_card/video_cmd`


top プロジェクトは、共有ライブラリとデモ アプリケーションを生成します。
* `./ws_of/gst/plugins/optical_flow/Debug/libgstsdxopticalflow.so`
* `./ws_of/gst/base/Debug/libgstsdxbase.so`
* `./ws_of/gst/allocators/Debug/libgstsdxallocator.so`
* `./ws_of/gst/apps/optical_flow/Debug/gstdemo.`

>**:information_source: ヒント:**
> * libopticalflow.so、libgstsdxbase.so、および libgstsdxallocator.so を lib ディレクトリにコピーします。
> * libgstsdxopticalflow.so を gstreamer-1.0 ディレクトリにコピーします。
> * 残りすべてのイメージを SD カードのルート フォルダーにコピーします。

**stereo の場合**

bottom ライブラリをビルドすると、sd_card ディレクトリに次のファイルが含まれます。
* `./ws_sv/stereo/Release/sd_card/image.ub`
* `./ws_sv/stereo/Release/sd_card/BOOT.BIN`
* `./ws_sv/stereo/Release/sd_card/libstereo.so`
* `./ws_sv/stereo/Release/sd_card/video_cmd`


top プロジェクトは、共有ライブラリとデモ アプリケーションを生成します。
* `./ws_sv/gst/plugins/stereo/Debug/libgstsdxstereo.so`
* `./ws_sv/gst/base/Debug/libgstsdxbase.so`
* `./ws_sv/gst/allocators/Debug/libgstsdxallocator.so`
* `./ws_sv/gst/apps/stereo/Debug/gstdemo.`

>**:information_source: ヒント:**
> * libstereo.so、libgstsdxbase.so、および libgstsdxallocator.so を lib ディレクトリにコピーします。
> * libgstsdxstereo.so を gstreamer-1.0 ディレクトリにコピーします。
> * 残りすべてのイメージを SD カードのルート フォルダーにコピーします。

**triple の場合**

bottom ライブラリをビルドすると、sd_card ディレクトリに次のファイルが含まれます。
* `./ws_triple/triple/Release/sd_card/image.ub`
* `./ws_triple/triple/Release/sd_card/BOOT.BIN`
* `./ws_triple/triple/Release/sd_card/libtriple.so`
* `./ws_triple/triple/Release/sd_card/video_cmd`


top プロジェクトは、共有ライブラリとデモ アプリケーションを生成します。
* `./ws_triple/gst/plugins/filter2d/Debug/libgstsdxfilter2d.so`
* `./ws_triple/gst/plugins/optical_flow/Debug/libgstsdxopticalflow.so`
* `./ws_triple/gst/plugins/stereo/Debug/libgstsdxstereo.so`
* `./ws_triple/gst/base/Debug/libgstsdxbase.so`
* `./ws_triple/gst/allocators/Debug/libgstsdxallocator.so`
* `./ws_triple/gst/apps/triple/Debug/gstdemo.`

>**:information_source: ヒント:**
> * SD カードのルート フォルダーに lib ディレクトリを作成し、その中に libtriple.so、libgstsdxbase.so、および libgstsdxallocator.so をコピーします。
> * libgstsdxfilter2d.so、libgstsdxstereo.so、および libgstsdxopticalflow.so を gstreamer-1.0 ディレクトリにコピーします。
> * 残りすべてのイメージを SD カードのルート フォルダーにコピーします。


* ターゲット ボードの SD カード スロットに SD カードを挿入します。
* ボードの電源をオンにします。数秒後に INIT_B LED とその横にある DONE LED が緑色になることを確認してください。
* コンピューターからシステムを制御します。TeraTerm、PuTTY などを使用してターミナル セッションを開始します。[セクション 6.1](tool-flow-tutorials.md#61-live_io-オプティカル-フロー-サンプル-アプリケーションのビルド) を参照してください。USB-UART ケーブルが接続され、ボードの電源がオンの状態なので、応答している COM ポートを見つけることができます。Linux ブートストラップおよびデバッグ メッセージが数ページ分表示され、最後に Linux コマンド ライン プロンプトが表示されます。
* cd コマンドを使用して `/media/card` ディレクトリに移動します。このディレクトリには、SD カードにコピーしたすべてのファイルが含まれます。
```
# cd /media/card

```
* 共有ライブラリを適切な場所にコピーします。
  * filter2d の場合:

	```
	# cp lib/libfilter2d.so /usr/lib
	# cp gstreamer-1.0/libgstsdxfilter2d.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxbase.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxallocator.so /usr/lib/gstreamer-1.0

	```
  * opticalflow の場合:

	```
	# cp lib/libopticalflow.so /usr/lib
	# cp gstreamer-1.0/libgstsdxopticalflow.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxbase.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxallocator.so /usr/lib/gstreamer-1.0

	```

  * stereo の場合:
	```

	# cp lib/libstereo.so /usr/lib
	# cp gstreamer-1.0/libgstsdxstereo.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxbase.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxallocator.so /usr/lib/gstreamer-1.0

	```

  * triple の場合:
	```

	# cp lib/libtriple.so /usr/lib
	# cp gstreamer-1.0/libgstsdxfilter2d.so /usr/lib/gstreamer-1.0
	# cp gstreamer-1.0/libgstsdxopticalflow.so /usr/lib/gstreamer-1.0
	# cp gstreamer-1.0/libgstsdxstereo.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxbase.so /usr/lib/gstreamer-1.0
	# cp lib/libgstsdxallocator.so /usr/lib/gstreamer-1.0

	```


**メディア パイプラインの初期化**

`video_cmd` ユーティリティを使用して使用可能なビデオ ソースをリストし、メディア パイプラインを設定します。これは、gstreamer デモ アプリケーションまたは `gst-launch` ユーティリティの前に実行する必要があります。
* 使用可能なビデオ ソース、そのソース ID および対応するビデオ ノードをリストするには、次のコマンドを使用します。
```

# video_cmd -S
    VIDEO SOURCE        ID         VIDEO DEVNODE
    MIPI CSI2 Rx        0       /dev/video3
      HDMI Input        1       /dev/video2
      USB Webcam        2       /dev/video4
Virtual Video De        3       /dev/video0

```

>**:pushpin: 注記:**
> 出力はボードに接続されているペリフェラルによるので、上記とは異なる場合があります。中央の列はソース ID を示しており、メディア パイプラインを初期化 (-s オプション) する次の手順で必要です。

MIPI、HDMI、および vivid ビデオ ソースでは、YUY2 および UYVY ピクセル フォーマットがサポートされています。USB では、サポートされるピクセル フォーマットはカメラのファームウェアによって異なります。たとえば、e-con USB カメラでは UYVY のみがサポートされますが、ZED ステレオ カメラでは YUYV (YUY2 と同一) がサポートされます。メディア パイプラインを設定する際は、入力パラメーターを正しく設定してください。

* MIPI メディア パイプラインを解像度 1920x1080、YUY2 ピクセル フォーマットに設定するには、次のコマンドを使用します。
```

# video_cmd -s 0 -i 1920x1080@YUY2 -X

```

  * `-s 0` は入力ソース ID で、この場合は MIPI CSI です。
  * `-i 1920x1080@YUY2` は、MIPI ソースを解像度 1080p、YUY2 フォーマットに設定します。
  * `-X` は、MIPI を設定した直後に `video_cmd` を終了します。
  * -s で選択した入力 ID に対応するビデオ ノードが返されます。ビデオ ノードは、デバイス プロパティを使用して v4lsrc プラグインに渡す必要があります。

* HDMI メディア パイプラインを解像度 1920x1080、UYVY ピクセル フォーマットに設定するには、次のコマンドを使用します。
```

# video_cmd -s 1 -i 1920x1080@UYVY -X

```

  * `-s 1` は入力ソース ID で、この場合は HDMI です。
  * `-i 1920x1080@UYVY` は、MIPI ソースを解像度 1080p、UVYV フォーマットに設定します。
  * `-X` は、HDMI を設定した直後に `video_cmd` を終了します。
  * -s で選択した入力 ID に対応するビデオ ノードが返されます。ビデオ ノードは、デバイス プロパティを使用して v4lsrc プラグインに渡す必要があります。

**ディスプレイ コントローラーの初期化**

`video_cmd` ユーティリティを使用してディスプレイ コントローラーを初期化します。コマンドは、バックグランドで実行する必要があります。そうしないと、`video_cmd` が終了した後にディスプレイ モードが元の値にリセットされます。これは、gstreamer デモ アプリケーションまたは `gst-launch` ユーティリティの前に実行する必要があります。

* DP ディスプレイ コントローラーの設定
```

# video_cmd -d 0 &

```

  * `-d 0` は、DP のディスプレイ ID です。

* HDMI ディスプレイ コントローラーを設定します。
```

# video_cmd -d 1 &

```

  * `-d 1` は、HDMI のディスプレイ ID です。

**Gstreamer アプリケーション**

gstreamer パイプラインを作成して実行するには、ソースからコンパイルされた gst デモ アプリケーションを使用するか、ビルド済みの `gst-launch` ユーティリティを使用します。

* コンパイル済みのデモ プログラムを使用するには、次のコマンドを実行します。
```

# ./gstdemo

```

  * デモ プログラムはすべて、ミキサーを介して HDMI 出力を使用します。
  * filter2d デモは HDMI 入力を使用します。
  * opticalflow デモは MIPI 入力を使用します。
  * stereo デモは USB ZED ステレオ カメラ入力を使用します。
  * triple の デモは上記すべての入力を使用します。

* 次の gst-launch コマンドは filter2d パイプラインを実行し、解像度 1920x1080、YUY2 フォーマットの MIPI からミキサー プレーン 29 を介して HDMI 出力を生成します。
```

gst-launch-1.0 \
    v4l2src device=/dev/video3 io-mode=dmabuf ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxfilter2d filter-preset=4 filter-mode=1 ! queue ! \
    kmssink bus-id=b00c0000.v_mix plane-id=29 sync=false fullscreen-overlay=true

```


* 次の gst-launch コマンドは opticalflow パイプラインを実行し、解像度 1920x1080、YUY2 フォーマットの HDMI からミキサー プレーン 29 を介して HDMI 出力を生成します。
```

gst-launch-1.0 \
    v4l2src device=/dev/video2 io-mode=dmabuf ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxopticalflow filter-mode=1 ! queue ! \
    kmssink bus-id=b00c0000.v_mix plane-id=29 sync=false fullscreen-overlay=true

```


* 次の gst-launch コマンドは opticalflow パイプラインを実行し、解像度 3840x1080 の並んだ入力、YUY2 フォーマットの HDMI からミキサー プレーン 29 を介して HDMI 出力を生成します。config-filename プロパティを誤使用のカメラのシリアル番号に置き換える必要があります。下の[ステレオ デモの詳細](#73-ステレオ-デモの詳細)を参照してください。
```

gst-launch-1.0 \
    v4l2src device=/dev/video4 io-mode=dmabuf ! \
    "video/x-raw, width=3840, height=1080, format=YUY2" ! \
    sdxstereo filter-mode=1 config-filename=/media/card/SN12263.conf ! queue ! \
    kmssink bus-id=b00c0000.v_mix plane-id=29 sync=false fullscreen-overlay=true

```


* 次は、秒ごとのフレーム数ディスプレイをイネーブルにして filter2d を実行しています。出力パイプ段は fpsdisplaysink で、先ほど使用した「kmssink....」文字列は video-sink という fpsdisplaysink プロパティの 1 つです。
```

gst-launch-1.0 \
    v4l2src device=/dev/video3 io-mode=dmabuf ! \
    "video/x-raw, width=1920, height=1080, format=YUY2" ! \
    sdxfilter2d filter-preset=4 filter-mode=1 ! queue ! \
    fpsdisplaysink video-sink="kmssink bus-id=b00c0000.v_mix plane-id=29 fullscreen-overlay=true" sync=false text-overlay=false -v

```


## 7.2 Gstreamer エレメント

これらのパイプラインは、エレメント **v4l2src**、**sdxfilter2d** (または **sdxopticalflow**、または **sdxstereo**)、**queue**、および **kmssink** を使用します。gstreamer ユーティリティ gst-inspect-1.0 を使用すると、これらのエレメントのプロパティおよびその他の情報を表示できます。

**v4l2src**

```

# gst-inspect-1.0 v4l2src

```

* 多くの情報が表示されます。v4l2src の device プロパティは、上記の各コマンドでビデオ ソースを選択するために設定されています。
  * /dev/video2 is HDMI
  * /dev/video3 is MIPI
  * /dev/video4 is US
* io-mode プロパティ
  * 4 は dmabuf で、パイプ段の間でイメージをコピーする必要はなく、フレームは参照で渡されることを示します。

* 最初の感嘆符 (!) は「video/x-raw, ....」です。これは、サポートされる多くのフォーマットのうちダウンストリームのパイプ エレメントに適したものがどれを v4l2src エレメントに通知します。具体的には、次を考慮します。
  * Raw ビデオ (非圧縮)
  * 幅と高さ
  * ピクセル フォーマット - YUY2 はピクセルごと 16 ビットの 4:2:2 で、Y が各ワードの下位バイトにあります。UYVY も 16 ビットの 4:2:2 ですが、Y が各ワードの上位バイトにあります。

**キュー**

これは必須ではありませんが、使用するとフレーム レートが高くなるので、パフォーマンスが向上します。

**kmssink**

kmssink プラグインを調べるには、次のコマンドを使用します。
```

# gst-inspect-1.0 kmssink

```

* bus-id プロパティ
  * b00c0000.v_mix は HDMI 出力 (ビデオ ミキサーを介する) を意味します。
  * fd4a0000.zynqmp-display は DP 出力を意味します。
* plane-id プロパティ
  * b00c0000.v_mix (HDMI 出力) を使用する場合:
       * 29 は YUY2 プレーンです。
       * 30 は YUY2 プレーンです。
       * 31 は UYUV プレーンです。
  * fd4a0000.zynqmp-display (DP 出力) を使用する場合:
       * 35 は RGB をサポートします。
       * 34 は YUY2 および UYVY をサポートします。

**sdx&lt;accelerator&gt;**

sdxfilter2d プラグインを調べるには、次のコマンドを使用します。
```

# gst-inspect-1.0 sdxfilter2d

```

* filter_mode プロパティ
  * 1: ハードウェア アクセラレーションを使用します。
  * 0: ソフトウェアを使用します (filter2d コードは完全に Arm プロセッサ上で実行)。
* filter_preset プロパティ
  * プリセット フィルターを選択します。1 ～ 10 の値を指定します。例では 4 に指定しており、エッジ強調フィルター (emboss) を使用しています。
* coefficients プロパティ
  * 3x3 係数マトリックスの配列です (例: `coefficients="<<0,0,0>,<0,-1,0>,<0,0,0>>"`)。

sdxopticalflow プラグインを調べるには、次のコマンドを使用します。
```

# gst-inspect-1.0 sdxopticalflow

```

* filter_mode プロパティ
  * 1: ハードウェア アクセラレーションを使用します。
  * 0: ソフトウェアを使用します (オプティカル フロー コードは完全に Arm プロセッサ上で実行)。

sdxstereo プラグインを調べるには、次のコマンドを使用します。
```

# gst-inspect-1.0 sdxstereo

```

* filter_mode プロパティ
  * 1: ハードウェア アクセラレーションを使用します。
  * 0: ソフトウェアを使用します (オプティカル フロー コードは完全に Arm プロセッサ上で実行)。
* config-filename プロパティ
  * ZED カメラ コンフィギュレーション ファイルを指定します。このファイルは、SD カードに存在する必要があります。[セクション 7.3](#73-ステレオ-デモの詳細) を参照してください。

## 7.3 ステレオ デモの詳細

ステレオ ビジョン デモは、複数の点から特別です。まず、USB ビデオ入力に接続されている ZED ステレオ カメラを使用する必要があります。次に、このアプリケーションに限り、入力画像解像度の幅が出力解像度の幅の 2 倍になっています。入力は 2 つの並んだ画像で構成されており、同期化された左および右ステレオ入力がカメラから供給されます。2560x720 を入力して 1280x720 を出力、3840x1080 を入力して 1920x1080 を出力する 2 つのモードが可能です。デフォルトの 3840x2160 出力解像度はステレオ ビジョン アプリケーションではサポートされていません。

このアプリケーションのもう 1 つ特別な点は、システムに接続されているカメラに対応する設定ファイルを使用する必要があるということです。各 StereoLabs ZED カメラには、特有のパラメーター ファイルが関連付けられています。このテキスト ファイルは StereoLabs から提供されているもので、ステレオ ビジョン デモを正しく機能させるためには、SD カードに存在する必要があります。特定のカメラ用のファイルは、シリアル番号 (ZED カメラの箱および ZED カメラの USB プラグの近くにある黒いタグに記載) から特定できます。シリアル番号は S/N 000012345 という形式であり、このカメラに対応するパラメーター ファイルは SN12345.conf という名前です。パラメーター ファイルをダウンロードするには、http://calib.stereolabs.com/?SN=12345 (12345 を実際のシリアル番号に置換) にアクセスします。

これにより、設定ファイルをコンピューターにダウンロードできます。

ステレオ ブロック マッチング アルゴリズムでは、人間が深度を認識するのと同様の方法である両眼視差に基づいて深度を計算します。深度マップは、擬色でコード記述されます。遠い物体は濃い青で示されます。物体が近くなるほど徐々に緑、黄、オレンジ、赤、紫と変化していき、最終的に 720p の場合はカメラから 2 フィート、1080p の場合はカメラから 5 フィートの距離にある物体が白で示されます。これより近い物体、および画像でテクスチャのない滑らかな領域は追跡できず、黒で表示されます。細部情報の多い (特に垂直エッジが多い) 部分が最も良く追跡できます。左側の大きな領域 (128 ピクセル幅) が黒であるのは普通で、これは双眼鏡の右と左の画像間でベスト マッチを水平検索するための領域を表します。



<hr/>

:arrow_forward:**次のトピック:**  [8.  プラットフォームの詳細](platform-details.md)

:arrow_backward:**前のトピック:**  [6.  ツール フロー チュートリアル](tool-flow-tutorials.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018 Xilinx</sup></p>
