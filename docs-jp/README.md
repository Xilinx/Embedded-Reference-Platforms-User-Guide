<p align="right">
            別の言語で表示: <a href="../README.md">英語</a>          
</p>
<table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://www.xilinx.com/content/dam/xilinx/imgs/press/media-kits/corporate/xilinx-logo.png" width="30%"/><h1>reVISION 入門ガイド 2018.3 (UG1265)</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center">1. はじめに</td>
    <td width="16%" align="center"><a href="./Docs/overview.md">2. 概要</a></td>
    <td width="17%" align="center"><a href="./Docs/software-tools-system-requirements.md">3. ソフトウェア ツールおよびシステム要件</a></td>
    <td width="17%" align="center"><a href="./Docs/design-file-hierarchy.md">4. デザイン ファイルの階層</a></td>
</tr>
<tr>
    <td width="17%" align="center"><a href="./Docs/operating-instructions.md">5. インストールおよび操作手順</a></td>
    <td width="16%" align="center"><a href="./Docs/tool-flow-tutorials.md">6. ツール フロー チュートリアル</a></td>
    <td width="17%" align="center"><a href="./Docs/run-application.md">7. アプリケーションの実行</a></td>
    <td width="17%" align="center"><a href="./Docs/platform-details.md">8. プラットフォームの詳細</a></td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="./Docs/known-issues-limitations.md">9. 既知の問題および制限</a></td>
    <td width="16%" align="center" colspan="2"><a href="./Docs/additional-references.md">10. その他のリソース</a></td>
</tr>
</table>

# 1. はじめに
ザイリンクス reVISION スタックは、プラットフォーム、アルゴリズム、およびアプリケーションを開発するためのさまざまな開発リソースを含みます。AlexNet、GoogLeNet、VGG、SSD、FCN などの人気の高いニューラル ネットワークのサポートも含まれます。さらに、定義済みおよび最適化済みの CNN ネットワーク層のインプリメンテーションを含むライブラリ エレメントが提供されています。機械学習エレメントには、コンピューター ビジョン処理用のアクセラレーション可能な OpenCV 関数が多数含まれます。アプリケーション レベルの開発に対しては、機械学習用の Caffe、コンピューター ビジョン用の OpenCV など、業界標準のフレームワークおよびライブラリがサポートされています。reVISION スタックには、さまざまなタイプのセンサーも含め、ザイリンクスおよびサードパーティからの開発プラットフォームも含まれます。詳細は、[ザイリンクス reVISION ウェブ ページ](http://japan.Xilinx.com/reVISION)を参照してください。

## 1.1. 改訂履歴
この入門ガイドは、次の reVISION プラットフォームの 2018.3 バージョン用です。
- ZCU102 シングル センサー
- ZCU104 シングル センサー
- 8 ストリーム VCU + CNN
- ZCU102 MIN
- ZCU104 MIN

ほかのバージョンの資料は、ザイリンクス Wiki の [reVISION 入門ガイド](http://www.wiki.xilinx.com/reVISION%20Getting%20Started%20Guide)からアクセスできます。

## 1.2. 変更履歴

**2018.3**
* 8 ストリーム VCU + CNN プラットフォームを追加
* 2018.3 SDSoC バージョンにアップデート
* 2018.3 xfOpenCV ライブラリ バージョンにアップデート
* 2018.3 Vivado バージョンにアップデート
* 2018.3 PetaLinux バージョンにアップデート
* `video_cmd` を削除し、新しい `xlnxvideosrc` および `xlnxvideosink` プラグインを追加
* マイナーな修正および改善


**2018.2**
* 2018.2 SDSoC バージョンにアップデート
* 2018.2 xfOpenCV ライブラリ バージョンにアップデート
* 2018.2 Vivado バージョンにアップデート
* 2018.2 PetaLinux バージョンにアップデート
* マイナーな修正および改善



## 1.3. サポート

このリファレンス デザインのテクニカル サポートが必要な場合は、[ザイリンクス アンサー データベース](https://japan.xilinx.com/support.html)から既知の問題のアンサーを検索してください。[ザイリンクス コミュニティ フォーラム](https://forums.xilinx.com/)では、技術的な詳細および問題に関する質問を投稿したり、ディスカッションに参加したりできます。新しいトピックを作成する前に、既に同様のトピックかないかどうかを確認してください。新しいトピックを作成する場合は、その問題または質問に適したサブフォーラム (例: Linux に関する質問は Embedded Linux) の下に作成してください。トピック名にプラットフォーム名 (ZCU102 reVISION、ZCU104 reVISION、8-stream VCU + CNN reVISION、または MIN reVISION) とリリース バージョンを含め、問題を簡潔に説明してください。

<hr/>

:arrow_forward:**次のトピック:** [2. 概要](./Docs/overview.md)

<hr/>
<p align="center"><sup>Copyright&copy; 2018-2019 Xilinx</sup></p>

この資料は表記のバージョンの英語版を翻訳したもので、内容に相違が生じる場合には原文を優先します。資料によっては英語版の更新に対応していないものがあります。日本語版は参考用としてご使用の上、最新情報につきましては、必ず最新英語版をご参照ください。