# ansible-playbook-test
Ansibleの動作確認用のサンプルplaybook。  
以下を環境に合わせて修正して実行する。  

- inventories/production/hosts：ansible_hostに設定するIPを変更
- inventories/staging/hosts：ansible_hostに設定するIPを変更
- inventories/production/group_vars/all.yml：SSH用のユーザ(ansible_ssh_user)、パスワード(ansible_ssh_pass)を変更
- inventories/staging/group_vars/all.yml：SSH用のユーザ(ansible_ssh_user)、パスワード(ansible_ssh_pass)を変更

## ディレクトリ構成
```
ansible
|-- ansible.cfg						# Ansibleの設定ファイル
|-- inventories						# インベントリと変数定義の格納場所
|   |-- production					# 商用環境用
|   |   |-- group_vars				# グループ単位の変数定義の格納場所
|   |   |   |-- all.yml				# 全グループ共通の変数定義
|   |   |   |-- test_group_a.yml	# グループごとの変数定義（ファイル名はグループ名.yml）
|   |   |   `-- test_group_b.yml
|   |   |-- host_vars				# ホスト単位の変数定義の格納場所
|   |   |   |-- test-prd-001.yml	# ホストごとの変数定義（ファイル名はホスト名.yml）
|   |   |   |-- test-prd-002.yml
|   |   |   `-- test-prd-003.yml
|   |   `-- hosts					# インベントリ(Ansibleの実行対象ホスト、グループの定義)
|   `-- staging						# ステージング環境用
|       |-- group_vars
|       |   |-- all.yml
|       |   |-- test_group_a.yml
|       |   `-- test_group_b.yml
|       |-- host_vars
|       |   `-- test-stg-001.yml
|       `-- hosts
|-- roles							# タスク定義の格納場所
|   |-- role00						# ロール単位でタスク定義をまとめている
|   |   |-- defaults
|   |   |   `-- main.yml			# ロールのデフォルト変数定義
|   |   `-- tasks
|   |       `-- main.yml			# タスクで実行したい処理をここに書く
|   |-- role01
|   |   |-- defaults
|   |   |   `-- main.yml
|   |   |-- tasks
|   |   |   `-- main.yml
|   |   |-- templates
|   |   |   `-- variable.txt.j2		# templateモジュールで使うテンプレートファイル
|   |   `-- vars
|   |       `-- main.yml			# ロール変数定義
|   `-- role02
|       |-- defaults
|       |   `-- main.yml
|       |-- tasks
|       |   `-- main.yml
|       |-- templates
|       |   `-- variable.txt.j2
|       `-- vars
|           `-- main.yml
|-- site.yml						# マスタープレイブック

|-- test_group_a.yml				# 実行対象のグループとロールを記載したプレイブック
`-- test_group_b.yml
```

## 実行例
### 商用環境に対し実行
$ ansible-playbook -i inventories/production/hosts site.yml  
### ステージング環境に対し実行
$ ansible-playbook -i inventories/staging/hosts site.yml
