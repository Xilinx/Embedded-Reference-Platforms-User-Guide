<p align="right">
            別の言語で表示: <a href="../master/Docs/overview.md">英語</a>    <table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>reVISION 入門ガイド 2018.2</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center"><a href="README.md">1. はじめに</a></td>
    <td width="16%" align="center">2. 概要</td>
    <td width="17%" align="center"><a href="software-tools-system-requirements.md">3. ソフトウェア ツールおよびシステム要件</a></td>
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

# 2.  概要

次の図に、reVISION シングル センサー デザインのブロック図を示します。
* ビデオ ソース (キャプチャ パイプライン) は青で示します。
* M2M (Memory-to-Memory) パイプラインとしてインプリメントされているコンピューター ビジョン アクセラレータは赤で示します。
* ビデオ シンク (出力/ディスプレイ パイプライン) は緑で示します。

![](./images/rv-ss-bd.jpg)

## 2.1 プラットフォーム

ZCU102/ZCU104 シングル センサー reVISION プラットフォームでは、次のビデオ インターフェイスがサポートされています。

### 2.1.1 ソース
* 1080p60 までの USB2/3 カメラまたはステレオ 1080p30
   * USB コントローラーは、プロセッシング システム (PS) の一部です。標準の Linux ユニバーサル ビデオ クラス (UVC) ドライバーを使用します。
* 4k60 までの HDMI Rx
   * HDMI キャプチャ パイプラインはプログラマブル ロジック (PL) にインプリメントされ、HDMI Rx Subsystem、Video Processing Subsystem (Scaler のみのコンフィギュレーション)、および Frame Buffer Write で構成されます。HDMI Rx Subsystem は、HDMI ソースから HDMI データ ストリームを受信してデコードし、AXI4-Stream に変換します。Video Processing Subsystem は、入力の色フォーマット (RGB、YUV444、YUV422 のいずれか) から YUV422 に変換し、オプションで画像をターゲットの解像度にスケーリングします。Frame Buffer Write IP は、YUV422 ストリームをパック形式の YUYV フォーマットとしてメモリに書き込みます。HDMI キャプチャ パイプラインは、V4L Linux フレームワークを使用します。
* 4k60 までのオプションの FMC カードを介した MIPI CSI
   * MIPI キャプチャ パイプラインは PL にインプリメントされ、ソニー IMX274 イメージ センサー、MIPI CSI2 Subsystem、Demosaic、Gamma、Video Processing Subsystem (CSC コンフィギュレーション)、Video Processing Subsystem (Scaler のみのコンフィギュレーション)、および Frame Buffer Write で構成されます。IMX274 イメージ センサーは、カメラ センサー インターフェイス (CSI) リンク を介して Raw 画像データを供給します。MIPI CSI2 Subsystem は、入力データ ストリームを受信してデコードし、AXI4-Stream に変換します。Demosaic IP は、Raw 画像フォーマットを RGB に変換します。Gamma IP は、チャネルごとのガンマ補正を実行します。VPSS-CSC は、色補正を実行します。VPSS Scaler は、RGB 画像を YUV422 に変換します。Frame Buffer Write IP は、YUV422 ストリームをパック形式の YUYV フォーマットとしてメモリに書き込みます。MIPI キャプチャ パイプラインは、V4L Linux フレームワークを使用します。

### 2.1.2 シンク
* 4k60 までの HDMI Tx
  * HDMI ディスプレイ パイプラインは PL にインプリメントされ、Video Mixer および HDMI Tx Subsystem で構成されます。Video Mixer は、メモリから 1 つの ARGB と 2 つの YUYV レイヤーを読み出します。提供されているデザイン例では、1 つの YUYV レイヤーのみが使用されます。この後ビデオ レイヤーが構成され、1 つの出力フレームにアルファブレンドされ、AXI4-Stream を介して HDMI Tx Subsystem に送信されます。HDMI Tx Subsystem は入力ビデオを HDMI データ ストリームにエンコードし、HDMI ディスプレイに送信します。HDMI ディスプレイ パイプラインは、DRM/KMS Linux フレームワークを使用します。
* 4k30 までの DP Tx
   * DP ディスプレイはデュアル レーン モード用に設定されており、PS の一部です。レイヤーごとにランタイム プログラマブルの色フォーマット コンバーターを含む単純な 2 レイヤー ブレンダーを含みます。2 つのレイヤーは、ターゲット ディスプレイの解像度に一致するフル スクリーンです。DP ディスプレイ パイプラインは、DRM/KMS Linux フレームワークを使用します。

## 2.2 デザイン例

### 2.2.1 ファイル I/O
これらは単純なデザイン例です。標準 OpenCV 読み出し (cv::imread() など) を使用して標準画像ファイルからビデオのフレームを読み出し、xfOpenCV 関数への呼び出しを使用してフレームを処理し、結果をファイルに出力します (cv::imwrite() を使用)。よく使用される OpenCV 関数のハードウェア アクセラレーションされたバージョンである xfOpenCV を 5 つ使用します。
* バイラテラル フィルター
* Harris フィルター
* 高密度オプティカル フロー
* ステレオ ビジョン (深度検出)
* ワープ変換

### 2.2.2 ライブ I/O
これらは、入力および出力ライブ ビデオの例です。
* 高密度オプティカル フロー - LI-IMX274MIPI-FMC **または** HDMI ソース **または** See3CAM_CU30 USB カメラが必要
   * このアルゴリズムは、時間的に連続する 2 つの画像を使用し、画像の各ピクセル位置における動きの方向と大きさを計算します。この計算は、オプティカル フロー見積もり用の Lucas–Kanade 法の単純なインプリメンテーションです。このオプティカル フロー アルゴリズムは、各ピクセル位置に対して、垂直方向の動きと水平方向の動きを表す 2 つの符号付きの値を返します。擬色出力の明るさは黒から鮮明な色までで、動きの大きさを表し、色は方向を示します。

* ステレオ ビジョン (深度検出) - ZED USB ステレオ カメラが必要
   * このアルゴリズムは、同じ時間に撮られたステレオ カメラからの 2 つの並んだ画像を使用し、画像の各ピクセル位置に対して深度 (カメラからの距離) を計算します。ステレオ ブロック マッチング アルゴリズムでは、人間が深度を認識するのと同様の方法である両眼視差に基づいて深度を計算します。深度マップは、擬色でコード記述されます。遠い物体は濃い青で示されます。物体が近くなるほど徐々に緑、黄、オレンジ、赤、紫と変化していき、カメラに最も近い物体は白で示されます。

* Filter2D - LI-IMX274MIPI-FMC **または** HDMI ソース **または** See3CAM_CU30 USB カメラが必要
   * たたみ込みは、ピクセルの強度を周辺ピクセルの強度を反映して変更する一般的な画像処理手法です。この手法は、ぼかし、鮮鋭化、エッジ検出などの画像効果を達成するため、画像フィルターに広く使用されます。インプリメントされたアルゴリズムでは、プログラム可能なフィルター係数を持つ 3x3 カーネルが使用されます。

* トリプル - 上記 3 つのデザインを 1 つのプロジェクトにまとめたものです (**ZCU102 のみ**)。
   * 3 つのデザインすべてをハードウェアで同時に使用できます。提供されるテスト アプリケーションでは、3 つの個別のビデオ ソースから、3 つのハードウェアでアクセラレーションされたプラグインを介して、HDMI ディスプレイに出力するためビデオ ミキサーの 3 つのプレーンに転送する 3 つのパイプラインが設定されます。

次の表に、サポートされるプラットフォームでのライブ I/O サンプルのパフォーマンス マトリックスを示します。

|   | **ZCU102** | **ZCU104** |
|----|----|----|
| **filter2d** | 2160p30 | 2160p30 |
| **optical_flow** | 2160p52 | 2160p30 |
| **stereo** | 1080p16 | 720p18 |

**:pushpin: 注記:**
ZCU104 のパフォーマンスを ZCU102 のレベルに引き上げるため取り組んでおります。

<hr/>

:arrow_forward:**次のトピック:**  [3.  ソフトウェア ツールおよびシステム要件](software-tools-system-requirements.md)

:arrow_backward:**前のトピック:**  [1.はじめに](README.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018 Xilinx</sup></p>
