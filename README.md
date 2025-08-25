# AWS Webサーバーデプロイプロジェクト

このプロジェクトは、Ansibleを使ってAWSのEC2インスタンスにWebサーバーを自動デプロイするものです。

##このプロジェクトの目的：Ansibleを使ってAWSサーバーにWebサーバーを自動デプロイするプロジェクトです。  
##作った理由：インフラ自動化の学習のため、Vagrantに続き、より実践的なAWS環境で検証を行いました。  
##動かし方：「hosts.ini」と「install_webserver.yml」を使って、Ansibleのコマンドで実行する方法を記載します。  
---
**手順**

1. AWS上での手順
**ステップ1: EC2インスタンスの準備
# まず、WebサーバーをデプロイするためのAWSのEC2インスタンスを立ち上げる必要があります。
AWSマネジメントコンソールにログイン: AWSアカウントを持っていない場合は、先に作成します。
EC2ダッシュボードへ移動: EC2インスタンスを起動する。OSは、Vagrantで使ったものと同じUbuntuを選ぶとスムーズです。
セキュリティグループの設定: SSH接続とWebアクセス（HTTP）を許可するように、セキュリティグループのルールを設定します。
SSH (ポート22): 君のPCのIPアドレスからのみ許可します。
HTTP (ポート80): どこからでもアクセスできるように許可します。
キーペアの作成: SSH接続に使うキーペアを作成して、秘密鍵（.pemファイル）をご自身のPCにダウンロードします。この秘密鍵は、AnsibleからのSSH接続に必要になるから、大切に保管してください。



---
# Troubleshooting
**1. `Permission denied` エラー**

# [誤]
[webservers]
XX.XX.XX.XX ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/your/aws-key.pem

# [正]
[webservers]
XX.XX.XX.XX ansible_user=ubuntu ansible_ssh_private_key_file=`"`/path/to/your/aws-key.pem`"`

**解決策:** `hosts.ini`ファイルに、秘密鍵のパスをダブルクォーテーションで囲んで指定することで解決しました。
