# ansible-playbook-test
Ansibleの動作確認用のサンプルplaybook。  
以下を環境に合わせて修正して実行する。  

- inventories/production/hosts：ansible_hostに設定するIPを変更
- inventories/staging/hosts：ansible_hostに設定するIPを変更
- inventories/production/group_vars/all.yml：SSH用のユーザ(ansible_ssh_user)、パスワード(ansible_ssh_pass)を変更
- inventories/staging/group_vars/all.yml：SSH用のユーザ(ansible_ssh_user)、パスワード(ansible_ssh_pass)を変更
