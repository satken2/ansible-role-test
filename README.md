# AnsibleのMoleculeのテスト

## テスト内容

以下のテストが実行されます。

- YAML LintによるYAMLのシンタックスチェック
- Ansible LintによるYAMLのシンタックスチェック
- Debianコンテナへのテスト実行
- Debianコンテナへのテスト実行(2回目)→冪等性の確認
- TestInfraでのチェック

## CI定義ファイル

`Jenkinsfile`にCIジョブの定義が入っています。

