# AWS Webサーバーデプロイプロジェクト

このプロジェクトは、Ansibleを使ってAWSのEC2インスタンスにWebサーバーを自動デプロイするものです。

##このプロジェクトの目的：Ansibleを使ってAWSサーバーにWebサーバーを自動デプロイするプロジェクトです。  
##作った理由：インフラ自動化の学習のため、Vagrantに続き、より実践的なAWS環境で検証を行いました。  
##動かし方：「hosts.ini」と「install_webserver.yml」を使って、Ansibleのコマンドで実行する方法を記載します。  

---

## Troubleshooting
**1. `Permission denied` エラー**

[誤]
[webservers]
# XX.XX.XX.XX
XX.XX.XX.XX ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/your/aws-key.pem

[正]
[webservers]
# XX.XX.XX.XX
XX.XX.XX.XX ansible_user=ubuntu ansible_ssh_private_key_file="/path/to/your/aws-key.pem"

**解決策:** `hosts.ini`ファイルに、秘密鍵のパスをダブルクォーテーションで囲んで指定することで解決しました。
