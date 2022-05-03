# Learn Terraform Functions

Learn what Terraform functions are and how to use them.

Follow along with the [Learn tutorial at HashiCorp Learn](https://learn.hashicorp.com/tutorials/terraform/functions?in=terraform/configuration-language).


## template関数
テンプレートファイルを読み込む
テンプレートファイル内にterraformの変数を設定することも可能

``` terraform
resource "aws_instance" "web" {
  user_data = templatefile("user_data.tftpl", { department = var.user_department, name = var.user_name })
}

```

※user_data.tftpl内にて${変数}のように変数を参照。
例）
sudo groupadd -r ${department}
sudo useradd -m -s /bin/bash ${name}
sudo usermod -a -G ${department} ${name}

## lookup関数
キーを指定して、マップから単一の要素の値を取得

```
# デプロイ
terraform apply -var "aws_region=us-east-2"

# 破棄
terraform destroy -var "aws_region=us-east-2"
```

## conkat関数
2つ以上のリストを受け取り、それらを1つのリストに結合

```
# SSHキーの生成
ssh-keygen -C "your_email@example.com" -f ssh_key

# デプロイ
terraform apply

# 8080ポートのセキュリティグループを確認
ssh ubuntu@$(terraform output -raw web_public_ip) -i ssh_key

# 破棄
terraform destroy

```
