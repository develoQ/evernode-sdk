# Evernode - Primer

## Apps vs dApps

アプリは、 **入力** を処理し、 **状態** の読み取り/更新中に **出力** を生成できるものと考えることができます。 従来のアプリの多くはこのカテゴリーに属し、市場にある多くのプログラミング言語やプラットフォームで実装することができます。

<img width="227" alt="image" src="https://user-images.githubusercontent.com/33562092/218354996-3b7315e3-b0dc-449f-9e17-14a02d16f83c.png" />

アプリの複数のインスタンスが一体となって動作し、入力、状態、出力を処理することで、**分散型**アプリ(dApp、別名スマートコントラクト)を作ることができます。 インスタンスを調整する単一の(中央の)組織はありません。 すべてのアプリのインスタンスは平等で、同じ動作をします。 アプリのインスタンスは、処理する内容がすべてのインスタンス間で一貫性があり、類似していることを互いに検証し、それぞれが同じ結果を生成します。

<img width="379" alt="image" src="https://user-images.githubusercontent.com/33562092/218356526-275fb1f6-1459-4412-9d38-1ec5931f10eb.png" />

コミュニケーションを取りながらお互いの動作を検証し、正しい結果に合意するプロセスを**コンセンサス**と呼びます。 このプロセスを行うリーダーや調整役はいません。 各アプリインスタンスはこの処理を個別に実行する必要があります。 HotPocketはあなたのアプリを「分散型」アプリにするために、この機能を提供します。

## HotPocketコンセンサスエンジン - 分散型アプリ用

HotPocket コンセンサスエンジンは、従来のプログラミングプラットフォームで書かれたPOSIX準拠アプリの分散化を支援するコンセンサスエンジンです。 HotPocketの用語では、各アプリケーションインスタンスは"**ノード**"です。 各ノードにはHotPocketソフトウェアとアプリケーションのコピーが含まれています。 あなたのアプリには、アプリケーションロジックと、HotPocketが制御および通信するために使用できるいくつかのインテグレーションポイントが含まれています。 HotPocket dAppsの作成方法については[チュートリアル](https://github.com/EvernodeXRPL/evernode-sdk#tutorials)をご覧ください。

- ユーザはあなたのアプリと通信するためにWebSocketを介してHotPocketと対話します。

- HotPocketはWebSocketを介して他のHotPocketノードとのコンセンサス処理を行います。

- HotPocketはあなたのアプリの次の部分を制御します。

  - コンセンサスプロセスに従って定期的にアプリを起動します。
  - あなたのアプリにユーザの一貫した入力を提供します。
  - アプリによって生成された出力や状態の変更を監視します。
  - 合意された出力を関連ユーザに返します。
  - ブロックチェーン台帳を管理し、アプリの動作を長期にわたって記録します。

- POSIX アプリケーション・ソフトウェアができることなら、何でも自由にできます。

  - インターネットに接続し、他のWebサービスとやり取りすることができます。
  - アプリケーションでは、従来のアプリケーションフレームワーク/ライブラリをすべて使用できます。
  - ファイルシステム(またはファイルベースのデータベース)をデータの永続化に使用できます。 HotPocketはファイルシステムを「状態」として扱います。
  - ユーザの入力と出力の生のバイナリデータを完全に制御できます。

- アプリは以下を遵守する必要があります。
  - アプリケーションロジックは **決定論的** でなければなりません。 与えられた**入力**と**状態**に対して、同一の**出力**を生成しなければなりません。 (例: マシンのタイムスタンプや乱数の使用はコンセンサスを壊す可能性があります)
  - Linux POSIX に準拠したアプリケーションである必要があります。
  - 必要なHotPocketの接続インターフェースを公開する必要があります。

<img width="421" alt="image" src="https://user-images.githubusercontent.com/33562092/218616038-001a3b46-4aed-4a3e-b410-ee0b2e8930b4.png" />

## Evernode - 分散型インフラ用

HotPocketを使用すると、分散型アプリを作成できます。 それらを実行するには、dAppノードをホストするために複数のマシン/ハードウェアが必要です。 dAppのインフラも分散型であることが理想的で、dAppノードが単一の組織に支配/所有されないようにする必要があります。 Evernodeはこれに必要な **分散型インフラストラクチャ** を提供します。 ホスティングリソースを提供し、HotPocket dAppsが利用できる[分散型マーケットプレイス](https://dashboard.evernode.org)です。

Evernodeは[XRPL Hooks](https://hooks.xrpl.org/)対応ネットワークを使って分散型マーケットプレイス活動を行います。 **ホスト** (ホスティングハードウェア) はマーケットプレイスに登録できます。 **テナント** は、 **Evers** (Evernodeのネイティブ通貨 - EVR)を使用して、いずれのホストからでもdAppホスティングリソースをリースできます。 リースされた各ホスティングインスタンスはHotPocketノードです。 テナントは、dAppファイルをHotPocketノードにデプロイします。 複数のHotPocketノードにリースしてデプロイすると、dAppクラスタが作成されます。

- Evernodeの **ホスト** と **テナント** はXRPLアカウントで表されています。
- マーケットプレイスの情報とルールは [XRPL Hooks](https://hooks.xrpl.org/) によって管理されています。
- マーケットプレースの操作(ホスト登録、リースなど)はXRPLトランザクションで表されます。
- 単一のホストは、ハードウェアリソースを使用して多くのdAppノードをリース可能にすることができます。
- dApp操作(デプロイ、コンセンサス、ユーザーインタラクション)は、WebSocketを介してHotPocketノードとユーザー間で直接行われます。 これらはXRPLネットワークに依存していません。 それらは単にホストによって割り当てられたネットワーク「ポート」を使うだけです([詳しく読む](https://github.com/EvernodeXRPL/evernode-host#firewalls-and-ports))。

次の図は、異なるHotPocket dAppsが多くのEvernodeホストに振り分けられる様子を表しています。 各dAppは独自のメッシュネットワークを形成します。

<img width="436" alt="image" src="https://user-images.githubusercontent.com/33562092/218644541-ff77330f-67cf-4962-96f9-e35c6d3e1c33.png" />

Evernodeホストになる方法は[こちら](https://github.com/EvernodeXRPL/evernode-host)をご覧ください。

## 参考リンク

- HotPocket - [コンセプト](hotpocket/concepts.md) | [チュートリアル](hotpocket/tutorial-basics.md)
- Sashimono - [コンセプト](https://github.com/EvernodeXRPL/evernode-host/blob/main/sashimono.md) | [アーキテクチャ](http://blog.geveo.com/Sashimono-Designing-a-multi-tenant-dApp-hosting-platform)
- [XRPL hooks](https://hooks.xrpl.org/)
