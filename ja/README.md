# Evernode SDK

EvernodeのSDKは、Evernode上でHotPocketスマートコントラクトを開発・展開するために必要なライブラリとツールで構成されています。 このレポは、開発途中のライブラリやツールにいち早くアクセスし、フィードバックを得るために使用されます。

Evernodeの概要については、 [Evernode-Primer](primer.md) をご覧ください。

## チュートリアル

HotPocketはEvernodeのスマートコントラクトの実行およびコンセンサスエンジンです。 HotPocketスマートコントラクトは、POSIX 準拠の言語/フレームワークを使用して開発できます。 また、Web Socketを使用してHotPocketスマートコントラクトとやり取りするクライアントアプリケーションを開発することもできます。 HotPocketの開発とEvernodeへの展開について理解するためには、以下の資料をご覧ください。

1. [HotPocket の概要](hotpocket/concepts.md)
2. [基礎チュートリアル](hotpocket/tutorial-basics.md)
3. [複数ノードの操作](hotpocket/tutorial-multinode.md)
4. [データの永続化](hotpocket/tutorial-persistdata.md)
5. [読み取りリクエスト](hotpocket/tutorial-readreq.md)
6. [NPLメッセージ](hotpocket/tutorial-npl.md)
7. [インスタンスの同期](hotpocket/tutorial-instance-sync.md)
8. [コントラクトの内容](hotpocket/contract-context.md)
9. [Evernodeへのコントラクトのデプロイ - シングルインスタンス](evernode/tutorial-basics.md)
10. [Evernodeへのコントラクトのデプロイ - インスタンスのクラスタ](evernode/tutorial-cluster.md)

## ツール

- hpdevkit - [HotPocket 開発者キット](hpdevkit/index.md) を使用して、ローカルのPCで HotPocketスマートコントラクトを簡単にテストできます。 上の [チュートリアル](#tutorials) に従って使い方を理解してください。
- evdevkit - [Evernode開発者キット](evdevkit/index.md) を使用してHotPocketスマートコントラクトをEvernodeホストに展開できます。 [Evernodeのチュートリアル](evernode/tutorial-basics.md) に従って使い方を理解してください。

## コード例

- [シンプルなechoコントラクト(nodejs)](https://github.com/HotPocketDev/hp-nodejs-contract/blob/main/example/echo-contract.js)
- [C言語のコントラクトの例](https://github.com/HotPocketDev/hp-c-contract/blob/main/example_contract.c)
- [Evernodeブートストラップコントラクト(C++)](https://github.com/HotPocketDev/evernode-bootstrap-contract)
- [Evernodeのjavascriptクライアントの使用例](https://github.com/HotPocketDev/evernode-js-client/blob/main/test/test.js)
- [計算機コントラクトとクライアントの例 (nodejs)](https://github.com/HotPocketDev/example-calculator-contract)

## ライブラリ

### HotPocketスマートコントラクトライブラリ

- [NodeJs ライブラリ](https://www.npmjs.com/package/hotpocket-nodejs-contract) ([ソース](https://github.com/HotPocketDev/hp-nodejs-contract))
- [C言語ライブラリ ソース](https://github.com/HotPocketDev/hp-c-contract)

### HotPocketクライアントライブラリ

- [nodejsとブラウザ用のJavascriptライブラリ](https://www.npmjs.com/package/hotpocket-js-client)。 ([ソース](https://github.com/HotPocketDev/hp-js-client))

### Evernodeクライアントライブラリ

- [nodejsとブラウザ用のJavascriptライブラリ](https://www.npmjs.com/package/evernode-js-client)。 ([ソース](https://github.com/HotPocketDev/evernode-js-client))
  - [共通クライアント機能](evernode/reference-api-common.md)
  - [Hookクライアントリファレンス](evernode/reference-api-hook-clients.md)
  - [テナントクライアント](evernode/reference-api-tenant.md)
  - [イベント](evernode/reference-api-events.md)

### EverPocket contract library

- [NodeJs library](https://www.npmjs.com/package/everpocket-nodejs-contract) ([source](https://github.com/EvernodeXRPL/everpocket-nodejs-contract))

### コミュニティライブラリ

- HotPocket用XRPLベースの分散型鍵管理フレームワーク DKM - [紹介](https://devpost.com/software/decentralized-key-management-evernode) | [ソース](https://github.com/wojake/DKM) (by [@wojake](https://github.com/wojake))

## プロトコルリファレンス

- [HotPocket設定リファレンス](hotpocket/reference-configuration.md)
- [HotPocketクライアントプロトコル](hotpocket/reference-client-protocol.md)
- [HotPocketコントラクトプロトコル](hotpocket/reference-contract-protocol.md)

## Issuerとフィードバック

何か問題やフィードバックがあれば、[こちら](https://github.com/HotPocketDev/evernode-sdk/issues)に投稿してください。

## アップデート

EvernodeSDKの最新情報を受け取るには[こちらから登録](https://github.com/HotPocketDev/evernode-sdk/issues/4)してください。
