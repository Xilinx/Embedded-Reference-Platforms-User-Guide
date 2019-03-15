<p align="right">
            別の言語で表示: <a href="../master/Docs/platform-details.md">英語</a>    <table style="width:100%"><table style="width:100%">
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
    <td width="17%" align="center"><a href="run-application.md">7. アプリケーションの実行</a></td>
    <td width="17%" align="center">8. プラットフォームの詳細</td>    
  </tr>
<tr>
    <td width="17%" align="center" colspan="2"><a href="known-issues-limitations.md">9. 既知の問題および制限</a></td>
    <td width="16%" align="center" colspan="2"><a href="additional-references.md">10. その他のリソース</a></td>
</tr>
</table>

# 8 プラットフォームの詳細

## 8.1 Vivado ハードウェア デザイン

Vivado ハードウェア デザインは、`zcu10[2|4]_[es2_]rv_ss/hw/zcu102_[es2_]rv_ss.dsa` にある DSA 内にパッケージされています。DSA には、使用可能な AXI インターフェイス、クロック、リセット、および割り込みを記述する hpfm ファイルも含まれます。Vivado でハードウェア デザインを開くには、[Tcl Console] で次のコマンドを実行します。

```
% open_dsa zcu10[2|4]_[es2_]rv_ss/hw/zcu10[2|4]_[es2_]rv_ss.dsa
```


## 8.2 PetaLinux BSP

PetaLinux BSP は、`zcu10[2|4]_[es2_]rv_ss/sw/petalinux_bsp` にあります。対応する Vivado プロジェクトからエクスポートした HDF ファイルは、PetaLinux BSP 内の `project-spec/hw-description/` サブフォルダーにあります。

PetaLinux BSP をコンフィギュレーションしてビルドするには、次のコマンドを実行します。

```
% cd petalinux
% petalinux-create -t project -s zcu102-prod-rv-ss.bsp -n bsp
% petalinux-config --get-hw-description=../zcu102_base_trd/hw --oldconfig
% petalinux-build
```

**:pushpin: 注記:** 特に PetaLinux プロジェクトが NFS マウントにある場合、tmp ディレクトリは別のフォルダーに移動されている可能性があります。PetaLinux の構成を確認してください。

生成された出力ファイルは、`images/linux/` サブフォルダーにあります。プラットフォームの一部としてパッケージされている関連ファイルは、次のとおりです。
* bl31.elf
* pmufw.elf
* u-boot.elf
* zynqmp_fsbl.elf
* image.ub

SDK/sysroot を生成するには、次のコマンドを実行します。

```
% petalinux-build -s
```

生成された SDK インストーラーは、`images/linux/sdk.sh` にあります。

## 8.3 ビデオ コマンド ライン ユーティリティ

ザイリンクス `video_cmd` ユーティリティは、関連の V4L2 キャプチャ デバイスのメディア パイプラインを初期化するために使用します。このユーティリティのビルド済みバージョンは `zcu10[2|4]_[es2_]rv_ss/sw/a53_linux/a53_linux/image/video_cmd` にあり、生成された SDx プロジェクトの `sd_card` フォルダーに自動的に配置されます。

`video_cmd`、`video_lib`、および `gst_lib` のソースは XSDK プロジェクトとして提供されており、`zcu10[2|4]_[es2_]rv_ss/workspaces/ws_video` に含まれます。次の手順に従って、SDx GUI を使用してアプリケーションをビルドします。

1. SDx を起動する前に、`SYSROOT` 環境変数が正しく設定されていることを確認してください。詳細は、デザイン例チュートリアルを参照してください。
2. SDx を起動し、ワークスペースとして `zcu10[2|4]_[es2_]rv_ss/workspaces/ws_video` ディレクトリを選択します。
3. SDx のメニューから [File] → [Import] → [General] → [Existing Projects into Workspace] をクリックします。[Next] をクリックします。
4. [Import Project] ダイアログ ボックスで、ワークスペースのルート ディレクトリ `zcu102_[es2_]rv_ss/workspaces/ws_video` に移動します。`gst_lib`、`video_lib`、および `video_cmd` プロジェクトのチェック ボックスがオンになっていることを確認し、[Finish] をクリックします。
5. [Project Explorer] ビューで追加した `video_cmd` プロジェクトを右クリックし、[Build Project] をクリックします。選択されているビルド コンフィギュレーションによって、`video_cmd` 出力ファイルは `Debug` または `Release` サブフォルダーに配置されます。

<hr/>

:arrow_forward:**次のトピック:**  [9.  既知の問題および制限](known-issues-limitations.md)

:arrow_backward:**前のトピック:**  [7.  アプリケーションの実行](run-application.md)
<hr/>
<p align="center"><sup>Copyright&copy; 2018 Xilinx</sup></p>
