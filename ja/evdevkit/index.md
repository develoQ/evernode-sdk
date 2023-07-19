# Evernode開発者キット
EvernodeはHotPocketをスマートコントラクトエンジンとして使用しています。 PC上でHotPocketスマートコントラクトを開発する場合、Evernode開発者キットを使用してEvernodeにデプロイすることができます。

## インストール

### 前提条件
Evernodeの開発者キットでは、開発マシンに [NodeJs](https://nodejs.org/en/) をインストールする必要があります。

### クロスプラットフォームのサポート
これはLinux と Windows の両方をサポートする npm グローバルパッケージです。
1. [前提条件](#prerequisites) をインストールします。
2. 以下のコマンドを実行して、ご使用のマシンに `evdevkit` をインストールします。
    ```
    npm i evdevkit -g
    ```

_**注記:** Linux プラットフォームでは、インストールには root 権限が必要です。 したがって、上記のコマンドに `sudo` を追加します。_

## Evernodeからのインスタンス取得
Evernode開発者キットを使ってEvernodeからインスタンスを取得することができます。 これにより、スマートコントラクトをデプロイできる新しいEvernodeインスタンスが作成されます。
- `EV_TENANT_SECRET` と `EV_USER_PRIVATE_KEY` [環境変数](#environment-variables) をインスタンスを取得する前に設定する必要があります。
- Evernodeインスタンスの設定を上書きするには [HotPocket設定](../hotpocket/reference-configuration.md) ファイルを作成し、パスを `EV_INSTANCE_CONFIG_PATH` [環境変数](#environment-variables) に設定します。
- 次のコマンドは、ランダムなホストにインスタンスを作成します。 指定された設定は `EV_INSTANCE_CONFIG_PATH` が与えられた場合に生成されます。
```
evdevkit acquire
```
- これは取得したインスタンスの詳細を返します。

## Evernodeへのコントラクトのデプロイ
既に実装されている [スマートコントラクト](../hotpocket/concepts.md#smart-contract) を、取得した Evernode インスタンスにデプロイできます。

### デプロイ可能なコントラクトパッケージの作成
evdevkitを使用してコントラクトをパッケージ化することができます。
- Evernodeインスタンスのコントラクト設定を上書きするには [コントラクト設定](../hotpocket/reference-configuration.md#contract) ファイルを作成し、そのパスを `EV_CONTRACT_CONFIG_PATH` [環境変数](#environment-variables) に設定します。
```
# evdevkit bundle <path to contract directory> <public key of the instance> <contract binary> -a <contract binary arguments>
evdevkit bundle $HOME/contract ed060ae0ec9183e4869e1490e908c9a9a9a3fd72816021c823ecd7d052e6e02d2 /usr/bin/node -a index.js
```
- 作成されたコントラクトバンドルへのパスが返されます。

### コントラクトをEvernodeにアップロード
コントラクトのバンドルを Evernode インスタンスにアップロードできます
- コントラクトをアップロードするには、 `EV_USER_PRIVATE_KEY` [環境変数](#environment-variables) を設定してください。
```
# evdevkit deploy <path to contract bundle> <IP of the instance> <User port of the instance>
evdevkit deploy $HOME/bundle/bundle.zip 45.76.238.97 26201
```

### テナント情報の変更
テナント情報を変更するには、[環境変数](#environment-variables)を上書きする必要があります：
1. HP_CLUSTER_SIZE 環境変数に必要なサイズを設定します。
    ```
    # Windows (command prompt)
    set EV_TENANT_SECRET=snmyH19JLWVaUJKtM4cNxTT6t38eA
    set EV_USER_PRIVATE_KEY=ed7b78ba4ffc9b7a55e427ff1ddb799ab1af59c6a9ab92e5f227815b04ab70e346831653e22c8293afac43694879c4083e1d7581b4326fcba423e3392e068028fe

    # Windows (powershell)
    $env:EV_TENANT_SECRET=snmyH19JLWVaUJKtM4cNxTT6t38eA
    $env:EV_USER_PRIVATE_KEY=ed7b78ba4ffc9b7a55e427ff1ddb799ab1af59c6a9ab92e5f227815b04ab70e346831653e22c8293afac43694879c4083e1d7581b4326fcba423e3392e068028fe

    # Linux (bash)
    export EV_TENANT_SECRET=snmyH19JLWVaUJKtM4cNxTT6t38eA
    export EV_USER_PRIVATE_KEY=ed7b78ba4ffc9b7a55e427ff1ddb799ab1af59c6a9ab92e5f227815b04ab70e346831653e22c8293afac43694879c4083e1d7581b4326fcba423e3392e068028fe
    ```
3. これで[acquire](#acquiring-instance-from-evernode)すると、新しいテナントからインスタンスが作成されます。

## 高度な使用方法
```
# Do [acquire](#acquiring-instance-from-evernode), [bundle](#creating-the-deployable-contract-package) and [deploy](#uploading-a-contract-to-evernode) in one command
evdevkit acquire-and-deploy <path to contract directory> <contract binary> -a <contract binary arguments>

# List the active hosts in Evernode
evdevkit list

# See host info
evdevkit host <host XRPL address>

# Generate user key pair
evdevkit keygen

# Create Evernode cluster and deploy a smart contract
evdevkit cluster-create <cluster size> <path to contract directory> <contract binary> -a <contract binary arguments>
```

HotPocketの設定例：
```json
{
    "contract": {
        "consensus": {
            "roundtime": 6000
        }
    },
    "mesh": {
        "peer_discovery": {
            "enabled": true,
            "interval": 10000
        }
    }
}
```

HotPocketコントラクトの設定例:
```json
{
    "consensus": {
        "roundtime": 2000
    }
}
```

_詳細は [HotPocket設定リファレンス](/hotpocket/reference-configuration.md) をご覧ください。_

## 環境変数
`evdevkit` CLI は以下の環境変数をサポートしています。

| 名前                        | 説明                                              |
| ------------------------- | ----------------------------------------------- |
| EV_TENANT_SECRET        | テナントのXRPLアカウントの秘密鍵。                             |
| EV_USER_PRIVATE_KEY     | コントラクトクライアントの秘密鍵(「evdevkit keygen」を使用して生成できます)。 |
| EV_INSTANCE_CONFIG_PATH | (任意) ローカルに作成されたHotPocketインスタンス構成ファイルのパス。        |
| EV_CONTRACT_CONFIG_PATH | (任意) ローカルに作成されたHotPocketコントラクト設定ファイルのパス。        |

## 更新
`evdevKit` を最新バージョンに更新するには、以下のコマンドを実行してください。
```
npm update evdevKit -g
```

## アンインストール
`evdevKit` をアンインストールするには、次のコマンドを実行します。

```
npm uninstall evdevkit -g
```

_**注記:** Linux プラットフォームでは、更新とアンインストールを実行するには、root 権限が必要です。 したがって、上記のコマンドに `sudo` を追加します。_

## 問題を報告する
[問題を報告する](https://github.com/HotPocketDev/evernode-sdk/issues).
