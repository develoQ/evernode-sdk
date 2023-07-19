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

### Viewing logs
You can re-enter the monitoring console with the command `hpdevkit logs 1`, where `1` is the HotPocket instance number you wish to monitor.

### Changing the cluster size
In order to resize the HotPocket cluster, you need to delete and re-create it:
1. Delete the existing cluster using the `hpdevkit clean` command.
2. Set the HP_CLUSTER_SIZE environment variable to the size you want.
    ```
    # Windows (command prompt)
    set HP_CLUSTER_SIZE=5

    # Windows (powershell)
    $env:HP_CLUSTER_SIZE=5

    # Linux (bash)
    export HP_CLUSTER_SIZE=5
    ```
3. Deploy your contract again with `npm start`.

## Creating HotPocket client application
You can use the HotPocket developer kit to generate a HotPocket client application such that everything is pre-configured. Here, we are creating a NodeJs client (This assumes you have prior experience with developing NodeJs applications):
```
hpdevkit gen nodejs blank-client myclient
cd myclient
npm install
node myclient.js
```
This will start the client application and connect a HotPocket node listening to port 8081. Also note that you need to have HotPocket nodes running on your machine for the client to connect.

## Advanced usage
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

If the contract files directory also contains a file named `hp.cfg.override`, it will be used to override the hp.cfg of all nodes. This can be used to set contract-specific parameters like 'bin_path' and 'bin_args'

An example `hp.cfg.override` file for a NodeJs application (the HotPocket developer kit NodeJs starter contract automatically includes this file for you):
```
{
    "contract": {
        "bin_path": "/usr/bin/node",
        "bin_args": "app.js"
    }
}
```

### Inspect contract files of all nodes
You can inspect the files of all the nodes of the cluster using Docker Desktop.
<img height="500" alt="image" src="https://user-images.githubusercontent.com/33562092/236630735-f39a3da0-78ca-4e91-9ef0-5c6400bd5bae.png" />


## Environment variables
`hpdevkit` CLI supports the following environment variables:

| Name                 | Description                                                                      | Default value                                   |
| -------------------- | -------------------------------------------------------------------------------- | ----------------------------------------------- |
| HP_CLUSTER_SIZE    | The number of nodes in the cluster. This only takes effect with a fresh cluster. | `3`                                             |
| HP_DEFAULT_NODE    | The node which the 'deploy' command uses to display logs.                        | `1`                                             |
| HP_DEVKIT_IMAGE    | The Docker image to be used for devkit cluster management.                       | `evernodedev/hpdevkit`                          |
| HP_INSTANCE_IMAGE  | The Docker image to be used for HotPocket instances.                             | `evernodedev/hotpocket:latest-ubt.20.04-njs.16` |
| HP_USER_PORT_BEGIN | The starting user port number for the cluster.                                   | `8081`                                          |
| HP_PEER_PORT_BEGIN | The starting peer port number for the cluster.                                   | `22861`                                         |

## Updates
Run one of the following commands to update `hpdevkit` to the latest version, and update the supporting docker images:
- Using hpdevkit CLI
    ```
    hpdevkit update
    ```

- Using npm
    ```
    npm update hpdevkit -g
    ```

**NOTE: You need to re-deploy your contracts for the new changes to take effect.**

## Uninstall
Run the following command to uninstall `hpdevkit` and the supporting docker images and containers:

- Using hpdevkit CLI
    ```
    hpdevkit uninstall
    ```

**NOTE: Uninstalling from hpdevkit CLI is recommended. If you uninstall using npm, you will have to clean the hpdevkit supporting docker images and containers manually.**

_**NOTE:** In Linux platforms, you will need root privileges to execute updates and uninstallations. Hence, add `sudo` to the above commands._

## Reporting issues
Report issues [here](https://github.com/HotPocketDev/evernode-sdk/issues).
