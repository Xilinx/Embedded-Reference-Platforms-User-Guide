<p align="right">
            別の言語で表示: <a href="../../Docs/known-issues-limitations.md">英語</a>    <table style="width:100%"><table style="width:100%">
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
    <td width="17%" align="center"><a href="run-application.md">7. アプリケーションの実行</a></td>
    <td width="17%" align="center"><a href="platform-details.md">8. プラットフォームの詳細</a></td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2">9. 既知の問題および制限</td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. その他のリソース</a></td>
</tr>
</table>

# 9. 既知の問題および制限

## 9.1. 既知の問題

* デバッグ コンフィギュレーションを使用した場合、SDSoC™ 環境アクセラレータ コードはソフトウェアのみのインプリメンテーションでは非常に低速に実行されます。

  **ソリューション:** プロジェクトのビルド コンフィギュレーションを [Release] に設定し、SDSoC コンパイラで最適化が最大限に実行されるように -O3 オプションを使用します。

* SDx プロジェクトを実行すると、次のような警告メッセージが表示されます。

  ```
  WARNING: [DMAnalysis 83-4492] Unable to determine the memory attributes passed to _mapx_mat.data of 
  function w1_xf_remap at /home/workspaces/ws_sv/stereo/src/stereo_sds.cpp:257, please use mem_attribute
  pragma to specify
  ```

  **ソリューション:** このメッセージは無視しても問題ありません。

## 9.2. 制限

* DisplayPort ケーブルと HDMI TX を同時に接続しないでください。
* ボードに電源を投入するときに、DisplayPort または HDMI TX ケーブルが差し込まれていることを確認してください。
* DP-to-HDMI アダプターはサポートされていません。[アンサー 67462](https://japan.xilinx.com/support/answers/67462.html) を参照してください。
* HDMI RX では次はサポートされません。
  * YUV 4:2:0 入力。
  * HDCP 暗号化入力。
  * アプリケーション実行中のホットプラグまたは動的な解像度の変更。
* 提供されている画像信号プロセッサ (ISP) パイプラインには自動アルゴリズムは含まれていません。IMX274、ガンマ、および色補正制御は、周囲の環境に基づいて手動で調整する必要があります。
* `optical_flow` ライブ I/O サンプルには、アルゴリズムのソフトウェア インプリメンテーションは含まれておらず、ハードウェアに最適化されたインプリメンテーションのみを使用可能です。
* SDSoC 環境では、`xfOpenCV` ライブラリおよび通常すべての C++ テンプレートのパフォーマンス見積もりはサポートされていません。パフォーマンス見積もりフローでまだサポートされていない部分は、関数テンプレートのソフトウェア パフォーマンスの見積もりです。ハードウェア リソースの HLS 見積もりが表示されると、SDSoC IDE とボード間のイーサネット P2P 通信が恒久的に停止し、エラー メッセージも表示されません。
* 8 ストリーム VCU + CNN プラットフォーム デモは、提供されている入力ファイルでのみテストされています。異なるエンコード レート、ファイル解像度/質、ストリーム数を使用する異なるファイルでは、結果が異なる場合があります。
* 効果的に使用するには、システムを完全に理解している必要があります。

<hr/>

:arrow_forward:**次のトピック:** [10. その他のリソース](additional-references.md)

:arrow_backward:**前のトピック:** [8. プラットフォームの詳細](platform-details.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018-2019 Xilinx</sup></p>
