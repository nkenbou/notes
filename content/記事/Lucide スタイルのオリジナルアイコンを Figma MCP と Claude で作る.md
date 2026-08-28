---
permalink: a3f8c2d91e7b
tags:
  - Figma
  - Claude
  - アイコン
  - OOUI
---
# Lucide スタイルのオリジナルアイコンを Figma MCP と Claude で作る

## きっかけ

「Nani翻訳」の作者 @catnose99 さんが X でこんな投稿をしていました。

https://x.com/catnose99/status/2011431510684111223

確かに Figma で図形を組み合わせれば SVG アイコンが作れます。ただ、手作業でやるのは手間です。

## Figma と Claude の連携

ちょうどこの頃、Figma と Claude（と Claude Code）の連携機能がリリースされました。

- [Create FigJam diagrams with Claude](https://help.figma.com/hc/en-us/articles/37883260397975-Create-FigJam-diagrams-with-Claude)
- [Guide to the Figma MCP server](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Figma-MCP-server)

Figma MCP サーバーを Claude Code に接続すると、Claude が Figma を直接操作できるようになります。セットアップは公式ドキュメントを参照してください。日本語での解説記事も参考になります。

- [Claude Code to Figma を使ってコードから Figma デザインを生成する – azukiazusa.dev](https://azukiazusa.dev/blog/claude-code-to-figma/)
- [Figma のキャンバスを AI エージェントから操作してデザインしよう – azukiazusa.dev](https://azukiazusa.dev/blog/use-figma-mcp-tool/)

Figma MCP が提供するツールのうち、アイコン作成に関係するものは主に2つです。

- `generate_figma_design` — プロンプトをもとに Figma 上に UI デザインを生成するツール
- `use_figma` — Figma Plugin API を通じて JavaScript を直接実行する汎用ツール。図形の配置・パスの描画など細かい操作が可能

この記事の実験では `use_figma` を使用しています。

Claude が Figma を操作できるなら、図形を組み合わせてアイコンを作れるのでは？と思って実験してみました。図形の組み合わせに限定すれば、期待通りのものが精度高く作れるはずという仮説です。

## 実験

### 自転車アイコン

プロンプト：

> Lucide のアイコンとして使用できるレベルの自転車 (bicycle) のアイコンを作成してください。

Claude は Lucide のスタイル（24×24px・strokeWidth 2・丸キャップ・塗りなし）を確認したうえで、前輪・後輪・フレーム・サドル・ハンドル・ペダルクランクを図形として配置しました。

Lucide の `bike`（参照用）：

![](<Lucide スタイルのオリジナルアイコンを Figma MCP と Claude で作る/figma-icon-bike.svg>)

Claude が生成した `bicycle`：

![](<Lucide スタイルのオリジナルアイコンを Figma MCP と Claude で作る/figma-icon-bicycle.svg>)

### 与信申請アイコン

プロンプト：

> 「与信申請」を表現したような Lucide のアイコンとして使えるレベルのアイコンを作成してください。

「与信申請 ＝ 申請書類＋信用審査」と解釈し、角折れ書類の右下に盾＋チェックマークのバッジを重ねた構成を提案・生成しました。

Claude が生成した `credit-application`（与信申請）：

![](<Lucide スタイルのオリジナルアイコンを Figma MCP と Claude で作る/figma-icon-credit-application.svg>)

## 実際の用途

OOUI を実践するとき、ドメインに即したアイコンが欲しい場面があります。OSS のアイコンセット（今回は Lucide をベース）は汎用的なものしかなく、ドメイン固有の概念は自分で作る必要があります。

自作する場合、既存のアイコンと組み合わせたときにスタイルがちぐはぐにならないよう合わせる手間がかかります。Lucide スタイルを指定すれば Claude がスタイルを揃えて生成してくれるため、この手間を省けます。

## まとめ

図形を組み合わせる範囲であれば、Claude は Figma 上でアイコンを精度高く生成できました。OSS アイコンにない概念を表現したいとき、Figma MCP を使って Claude に依頼するのは有効な手段だと感じました。
