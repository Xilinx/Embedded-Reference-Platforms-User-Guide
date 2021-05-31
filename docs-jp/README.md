<p align="right">
            別の言語で表示: <a href="../README.md">英語</a>          
</p>
<table style="width:100%">
  <tr>

<th width="100%" colspan="6"><img src="https://github.com/Xilinx/Image-Collateral/blob/main/xilinx-logo.png?raw=true" width="30%"/><h1>reVISION 入門ガイド 2018.2</h1>
</th>

  </tr>
  <tr>
    <td width="17%" align="center">1. はじめに</td>
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
    <td width="17%" align="center" colspan="2"><a href="known-issues-limitations.md">9. 既知の問題および制限</a></td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. その他のリソース</a></td>
</tr>
</table>

# 1.  はじめに
ザイリンクス reVISION スタックは、プラットフォーム、アルゴリズム、およびアプリケーションを開発するためのさまざまな開発リソースを含みます。AlexNet、GoogLeNet、VGG、SSD、FCN などの人気の高いニューラル ネットワークのサポートも含まれます。さらに、定義済みおよび最適化済みの CNN ネットワーク層のインプリメンテーションを含むライブラリ エレメントが提供されています。機械学習エレメントには、コンピューター ビジョン処理用のアクセラレーション可能な OpenCV 関数が多数含まれます。アプリケーション レベルの開発に対しては、機械学習用の Caffe、コンピューター ビジョン用の OpenCV など、業界標準のフレームワークおよびライブラリがサポートされています。reVISION スタックには、さまざまなタイプのセンサーも含め、ザイリンクスおよびサードパーティからの開発プラットフォームも含まれます。詳細は、[ザイリンクス reVISION ウェブ ページ](http://japan.Xilinx.com/reVISION)を参照してください。

## 1.1 改訂履歴
この入門ガイドは、**ZCU102** および **ZCU104** シングル センサー reVISION プラットフォームの **2018.2** バージョン用です。ほかのバージョンの資料は、[reVISION 入門ガイド](http://www.wiki.xilinx.com/reVISION%20Getting%20Started%20Guide)からアクセスできます。

## 1.2 変更ログ

**2018.2**
* 2018.2 SDSoC バージョンにアップデート
* 2018.2 xfOpenCV ライブラリ バージョンにアップデート
* 2018.2 Vivado バージョンにアップデート
* 2018.2 PetaLinux バージョンにアップデート
* マイナーな修正および改善

## 1.3 サポート

このリファレンス デザインのテクニカル サポートが必要な場合は、次のリソースをご利用ください。
* [ザイリンクス アンサー データベース](https://japan.xilinx.com/support.html): 既知の問題のアンサー
* [ザイリンクス コミュニティ フォーラム](https://forums.xilinx.com/): 技術的な詳細および問題に関する質問およびディスカッション。新しいトピックを作成する前に、既存のトピックを検索するようにしてください。新しいトピックを作成する場合は、その問題または質問に適したサブフォーラム (例: Linux に関する質問は Embedded Linux) の下に作成してください。トピック名には、問題の簡単な説明と共に、「ZCU102 reVISION」または「ZCU104 reVISION」とリリース バージョンを含めてください。

<hr/>

:arrow_forward:**次のトピック:**  [2.  概要](overview.md)

<hr/>
<p align="center"><sup>Copyright&copy; 2018 Xilinx</sup></p>

この資料は表記のバージョンの英語版を翻訳したもので、内容に相違が生じる場合には原文を優先します。資料によっては英語版の更新に対応していないものがあります。日本語版は参考用としてご使用の上、最新情報につきましては、必ず最新英語版をご参照ください。
