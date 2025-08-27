# Ansible Webサーバー構築 Playbook
このPlaybookは、AWS上のEC2インスタンスにWebサーバー（Apache）を自動で構築するためのものです。

1. プロジェクト概要
このリポジトリには以下の2つのファイルが含まれています。

・inventory.ini: ターゲットとなるサーバーの情報を記載  
・playbook.yml: サーバー構築の手順を定義

3. 事前準備
このPlaybookを実行する前に、以下の準備が必要です。

・Ansibleのインストール: Ansibleが実行できる環境を用意してください。  
・AWS CLIの設定: AWSアカウントの認証情報が設定済みであることを確認してください。  
・SSHキーペア: EC2インスタンスに接続するためのキーペア（.pemファイル）を用意してください。  

4. 実行方法

以下のコマンドを実行することで、Webサーバーが構築されます。

ansible-playbook -i inventory.ini playbook.yml

5. Playbookの内容
inventory.ini
実行対象のEC2インスタンスのパブリックIPアドレスまたはDNS名を[webservers]グループに記載します。

[webservers]
## ここにEC2インスタンスのDNS名またはパブリックIPアドレスを記載
ec2-xx-xx-xx-xx.ap-northeast-1.compute.amazonaws.com ansible_ssh_private_key_file=/path/to/your-key.pem ansible_user=ec2-user
```ansible_ssh_private_key_file`には、SSHキーペアのパスを、`ansible_user`には、接続するユーザー名（例：Amazon Linuxの場合は`ec2-user`）をそれぞれ指定します。

#### `playbook.yml`

Playbookは以下のタスクを実行します。

1.  **`name: Install Apache`**: `yum`コマンドでApacheをインストールします。
2.  **`name: Copy index.html`**: Webサーバーに表示する`index.html`を配置します。
3.  **`name: Start and enable httpd service`**: Apacheサービスを起動し、サーバー起動時に自動で立ち上がるように設定します。
4.  **`name: Check httpd status`**: Apacheサービスが正常に起動しているか確認します。

---
