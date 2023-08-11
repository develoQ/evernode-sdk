# HotPocket開発者キット

EvernodeはHotPocketをスマートコントラクトエンジンとして使用しています。 HotPocketスマートコントラクトは、POSIX 準拠の言語/フレームワークを使用して開発できます。 HotPocket開発者キットを使用すると、ローカルPC上で簡単にHotPocketスマートコントラクトの開発およびテストができます。

## インストール

### 前提条件

HotPocket開発者キットでは、開発マシンに [Docker Engine](https://docs.docker.com/engine/install/) と [NodeJs](https://nodejs.org/en/) をインストールする必要があります。

### クロスプラットフォーム対応

HotPocket開発者キットは、LinuxとWindowsの両方のオペレーティングシステムをサポートする [グローバルnpmパッケージ](https://www.npmjs.com/package/hpdevkit) です。

1. [前提条件](#prerequisites) をインストールします。
2. 次のコマンドを実行して、お使いのマシンに hpdevkit をインストールします。
   ```
   npm i hpdevkit -g
   ```

_**注記:** Linux プラットフォームでは、インストールには root 権限が必要です。 したがって、上記のコマンドに `sudo` を追加します。_

## HotPocketスマートコントラクトの作成

HotPocket開発者キットを使用して、事前に設定されたスマートコントラクトプロジェクトを生成することができます。 ここでは、Node.js のスマートコントラクトを作成します(これは、Node.js アプリケーションの開発経験があることを前提としています)。

```
hpdevkit gen nodejs starter-contract myproj
cd myproj
npm install
npm start
```

'npm start' コマンドは、NodeJs のスマートコントラクトをビルドし、マシン上で実行されている HotPocket クラスタにデプロイします。 また、HotPocketインスタンスからコンソール出力を出力します。 Ctrl+C を押すといつでもHotPocketコンソール出力の監視を終了することができます。 ただし、監視コンソールを終了した後もHotPocketインスタンスは引き続き実行されます。

### ログの表示

`hpdevkit logs 1`（`1`は監視したいHotPocketインスタンス番号）コマンドで監視コンソールに再度入ることができます。

### クラスタサイズの変更

HotPocketクラスタのサイズを変更するには、削除して再作成する必要があります。

1. `hpdevkit clean` コマンドを使用して既存のクラスタを削除します。
2. HP_CLUSTER_SIZE 環境変数に必要なサイズを設定します。

   ```
   # Windows (command prompt)
   set HP_CLUSTER_SIZE=5

   # Windows (powershell)
   $env:HP_CLUSTER_SIZE=5

   # Linux (bash)
   export HP_CLUSTER_SIZE=5
   ```

3. `npm start` で再度コントラクトをデプロイします。

## HotPocketクライアントアプリケーションの作成

HotPocket開発者キットを使用して、事前に設定されたHotPocketクライアントアプリケーションを生成することができます。 ここでは、Node.js クライアントを作成します(これは、Node.js アプリケーションの開発経験があることを前提としています)。

```
hpdevkit gen nodejs blank-client myclient
cd myclient
npm install
node myclient.js
```

これによりクライアントアプリケーションが起動し、ポート8081をリッスンしているHotPocketノードに接続します。 クライアントが接続するには、マシン上でHotPocketノードが実行されている必要があります。

## 高度な使用方法

```
# Deploy contract files directory to the cluster (`npm start` internally uses this command to deploy)
hpdevkit deploy <contract files directory>

# Stop and clean-up everything (required for changing cluster size)
hpdevkit clean

# View a specific node's logs
hpdevkit logs <node number>

# Start/stop all nodes
hpdevkit start
hpdevkit stop

# Start/stop a specific node
hpdevkit start <node number>
hpdevkit stop <node number>

# Add a new node to the cluster
# (The new node will use the existing UNL and become an observer node)
hpdevkit spawn
```

コントラクトファイルディレクトリに`hp.cfg.override`というファイルがある場合、そのファイルはすべてのノードのhp.cfgを上書きするために使われます。 'bin_path' や 'bin_args' のようなコントラクト固有のパラメータを設定するために使用できます。

NodeJs アプリケーション用の `hp.cfg.override` ファイルの例 (HotPocket 開発キット NodeJs スターターコントラクトには、このファイルが自動的に含まれています):

```
{
    "contract": {
        "bin_path": "/usr/bin/node",
        "bin_args": "app.js"
    }
}
```

### すべてのノードのコントラクトファイルを調べる

Docker Desktopを使用して、クラスタのすべてのノードのファイルを調べることができます。
<img height="500" alt="image" src="https://user-images.githubusercontent.com/33562092/236630735-f39a3da0-78ca-4e91-9ef0-5c6400bd5bae.png" />

## 環境変数

`hpdevkit` CLI は以下の環境変数をサポートしています。

| 名前                   | 説明                               | デフォルト値                                          |
| -------------------- | -------------------------------- | ----------------------------------------------- |
| HP_CLUSTER_SIZE    | クラスタ内のノード数。 これは新しいクラスタでのみ有効です。   | `3`                                             |
| HP_DEFAULT_NODE    | 'deploy' コマンドがログを表示するために使用するノード。 | `1`                                             |
| HP_DEVKIT_IMAGE    | devkitクラスタ管理に使用するDockerイメージ。     | `evernodedev/hpdevkit`                          |
| HP_INSTANCE_IMAGE  | HotPocketインスタンスに使用するDockerイメージ。  | `evernodedev/hotpocket:latest-ubt.20.04-njs.20` |
| HP_USER_PORT_BEGIN | クラスタの開始ユーザポート番号。                 | `8081`                                          |
| HP_PEER_PORT_BEGIN | クラスタの開始ピアポート番号。                  | `22861`                                         |

## 更新

以下のいずれかのコマンドを実行して、 `hpdevkit` を最新バージョンに更新し、サポートされているdocker imagesを更新します。

- hpdevkit CLI を使用する

  ```
  hpdevkit update
  ```

- npm を使用する
  ```
  npm update hpdevkit -g
  ```

**注記: 新しい変更を有効にするには、コントラクトを再デプロイする必要があります。**

## アンインストール

以下のコマンドを実行して、 `hpdevkit` とサポートされているdocker イメージとコンテナをアンインストールします。

- hpdevkit CLI を使用する
  ```
  hpdevkit uninstall
  ```

**注記: hpdevkit CLI からアンインストールすることを推奨します。 npm を使用してアンインストールする場合、docker イメージとコンテナをサポートする hpdevkit を手動でクリーンアップする必要があります。**

_**注記:** Linux プラットフォームでは、更新とアンインストールを実行するには、root 権限が必要です。 したがって、上記のコマンドに `sudo` を追加します。_

## 問題を報告する

[問題を報告する](https://github.com/HotPocketDev/evernode-sdk/issues).
