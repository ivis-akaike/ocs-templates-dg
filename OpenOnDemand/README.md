# VcpSDKを利用したOpenOnDemandのセットアップ

このテンプレートでは、VcpSDKを利用してOpenOnDemandをインストール・セットアップします。

Open OnDemandは、Web UI経由でジョブ投入を可能にするWebアプリケーションです。Jupyter NotebookなどのようなWebアプリケーションをジョブとして動作させることもサポートしています。

## 概要

[OpenHPC-v2テンプレート](../OpenHPC-v2/)を用いて作成されたOpenHPC/Slurmクラスタに対し、[Open OnDemand](https://openondemand.org/)をインストール・セットアップします。

なお、セットアップにあたっては、OpenHPC-v2テンプレートで作成したgroup_varsとansibleの設定を再利用します。

このテンプレートによる動作確認を実施したクラウド環境は、現在のところmdxのみです。

## システム構成

![](images/ohpc%2Bood.svg)

Open OnDemandは原則としてHPCクラスタのログインノードにインストールするもののため、OpenHPC-v2テンプレートで作成したSlurmクラスタでは、マスターノードにインストールします。

Open OnDemandはOpenHPCと同様、VCノードのBaseコンテナにインストールします。

## 要件

* OpenHPCの構築時と同様、Jupyter NotebookからVcpSDKを用いてVCコントローラにアクセスし、VCノードの制御ができること。
* OpenHPC-v2テンプレートに基いてOpenHPC/Slurmクラスタが構築済みであること。構築の際に作成されたgroup_varsとansibleの設定が残っていること。
* サーバ証明書を用意してHTTPSサーバをセットアップすれば、マスターノードにHTTPSでアクセス可能な状態にあること。Open OnDemandではHTTPSは必須ではないとしているものの、HTTPでは正しく動作しない機能が多く、ほぼ使いものにならない。

## Notebookの使用方法

[このREADMEのあるディレクトリ](./)にあるNotebookを直接開いて使用してください。以下の順に実行することで、Open OnDemandのWeb UIからバッチジョブ実行が可能となります。

1. [010-OpenOnDemandのインストール](./010-OpenOnDemand%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB.ipynb)
1. [020-OpenOnDemandのセットアップ](./020-OpenOnDemand%E3%81%AE%E3%82%BB%E3%83%83%E3%83%88%E3%82%A2%E3%83%83%E3%83%97.ipynb)
1. [030-OpenOnDemandにジョブ実行環境(Slurm)をセットアップする](./030-OpenOnDemand%E3%81%AB%E3%82%B8%E3%83%A7%E3%83%96%E5%AE%9F%E8%A1%8C%E7%92%B0%E5%A2%83%28Slurm%29%E3%82%92%E3%82%BB%E3%83%83%E3%83%88%E3%82%A2%E3%83%83%E3%83%97%E3%81%99%E3%82%8B.ipynb)

「[040-正常性確認用ジョブの実行](./040-%E6%AD%A3%E5%B8%B8%E6%80%A7%E7%A2%BA%E8%AA%8D%E7%94%A8%E3%82%B8%E3%83%A7%E3%83%96%E3%81%AE%E5%AE%9F%E8%A1%8C.ipynb)」は、Open OnDemandのWeb UIからのバッチジョブ実行方法を示したものです。このNotebookにはコード部分は存在せず、ドキュメントのみです。

「[050-ComputeNodeにJupyterNotebookをセットアップする](./050-ComputeNode%E3%81%ABJupyterNotebook%E3%82%92%E3%82%BB%E3%83%83%E3%83%88%E3%82%A2%E3%83%83%E3%83%97%E3%81%99%E3%82%8B.ipynb)」のNotebookは、Jupyter Notebookサーバをジョブとして実行するための設定を示したものです。通常のバッチジョブを実行するだけであれば、実行する必要はありません。